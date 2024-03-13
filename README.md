from flask import Flask, request, render_template
import pandas as pd
import os

app = Flask(__name__)
if not os.path.exists('uploads'):
    os.makedirs('uploads')

business_types = [
    "Food Manufacturers and Nutrition Consultancy",
    "Food Processing Machinery",
    "IT",
    "Stationery and Branding",
    "Trader",
    "Banking and Investment Services",
    "Software and Web Development",
    "Accommodation and Conference Facility",
    "Transportation and logistics",
    "Fuel and Pumps",
    "Warehouse"
]

# Define profit margin ranges for each business type
profit_margin_ranges = {
    "Food Manufacturers and Nutrition Consultancy": {
        "gross": "20% to 40%",
        "operating": "10% to 20%",
        "net": "5% to 15%",
        "return": "5% to 15%"
    },
    "Food Processing Machinery": {
        "gross": "25% to 45%",
        "operating": "10% to 20%",
        "net": "5% to 15%",
        "return": "5% to 15%"
    },
    "IT": {
        "gross": "50% and greater",
        "operating": "10% to 30%",
        "net": "10% to 30%",
        "return": "5% to 15%"
    },
    "Stationery and Branding": {
        "gross": "10% to 20%",
        "operating": "10% to 20%",
        "net": "10% to 20%",
        "return": "5% to 15%"
    },
    "Trader": {
        "gross": "-50% to 50%",
        "operating": "-50% to 30%",
        "net": "-50% to 30%",
        "return": "10% and greater"
    },
    "Banking and Investment Services": {
        "gross": "20% to 40%",
        "operating": "20% to 40%",
        "net": "10% to 25%",
        "return": "0.5% to 2.5%"
    },
    "Software and Web Development": {
        "gross": "50% and greater",
        "operating": "10% to 30%",
        "net": "10% to 30%",
        "return": "25% and greater"
    },
    "Accommodation and Conference Facility": {
        "gross": "50% to 70%",
        "operating": "10% to 30%",
        "net": "5% to 15%",
        "return": "5% to 15%"
    },
    "Transportation and logistics": {
        "gross": "10% to 30%",
        "operating": "3% to 10%",
        "net": "2% to 8%",
        "return": "5% to 15%"
    },
    "Fuel and Pumps": {
        "gross": "5% to 15%",
        "operating": "2% to 8%",
        "net": "1% to 5%",
        "return": "2% to 10%"
    },
    "Warehouse": {
        "gross": "10% to 30%",
        "operating": "5% to 15%",
        "net": "2% to 10%",
        "return": "5% to 15%"
    }
}
# app = Flask(__name__)
# if not os.path.exists('uploads'):
#     os.makedirs('uploads')

# Define a generic calculate_metrics function that accepts a business type parameter
def calculate_metrics(file_path, business_type):
    # Read the CSV file
    data = pd.read_csv(file_path, header=None)
 
    # Check the shape
    num_columns = data.shape[1]
    if num_columns != 6:
        raise ValueError(f"Expected 6 columns in the CSV but got {num_columns}")

    # Assuming first row is headers, extract them and then drop the first row
    headers = data.iloc[0].tolist()
    data = data.drop(0).reset_index(drop=True)

    # Use extracted headers for column names
    data.columns = headers

    # Fetch data from dataframe
    gross_profit = float(data['Gross Profit'].replace(',', ''))
    revenue = float(data['Revenue'].replace(',', ''))
    operating_profit = float(data['Operating Profit'].replace(',', ''))
    net_profit = float(data['Net Profit'].replace(',', ''))
    net_income = float(data['Net Income'].replace(',', ''))
    avg_total_assets = float(data['Avarage Total Assets'].replace(',', ''))
    print(gross_profit,revenue,operating_profit,net_profit,net_income,avg_total_assets)
    # Initialize result dictionary
    results = {}

    # Add business type-specific calculations
    if business_type == "Food Manufacturers and Nutrition Consultancy":
        # Calculate ratios specific to this business type
        Gross_Profit_Margin = (gross_profit / revenue) * 100
        Operating_Profit_Margin = (operating_profit / revenue) * 100
        Net_Profit_Margin = (net_profit / revenue) * 100
        Return_on_Assets = (net_income / avg_total_assets) 
        
        # Add your calculations here
        results["Gross Profit Margin"] = Gross_Profit_Margin
        results["Operating Profit Margin"] = Operating_Profit_Margin
        results["Net Profit Margin"] = Net_Profit_Margin
        results["Return on Assets"] = Return_on_Assets

    elif business_type == "Food Processing Machinery":
        # Calculate ratios specific to this business type
        Gross_Profit_Margin = (gross_profit / revenue) * 100
        Operating_Profit_Margin = (operating_profit / revenue) * 100
        Net_Profit_Margin = (net_profit / revenue) * 100
        Return_on_Assets = (net_income / avg_total_assets)
        # Add your calculations here
        results["Gross Profit Margin"] = Gross_Profit_Margin
        results["Operating Profit Margin"] = Operating_Profit_Margin
        results["Net Profit Margin"] = Net_Profit_Margin
        results["Return on Assets"] = Return_on_Assets
        
    elif business_type == "IT":
        # Calculate ratios specific to the "IT" business type
        Gross_Profit_Margin = (gross_profit / revenue) * 100
        Operating_Profit_Margin = (operating_profit / revenue) * 100
        Net_Profit_Margin = (net_profit / revenue) * 100
        Return_on_Assets = (net_income / avg_total_assets) 
        # Add your calculations here
        results["Gross Profit Margin"] = Gross_Profit_Margin
        results["Operating Profit Margin"] = Operating_Profit_Margin
        results["Net Profit Margin"] = Net_Profit_Margin
        results["Return on Assets"] = Return_on_Assets
        

    elif business_type == "Stationery and Branding":
        
        # Calculate ratios specific to the "Branding" business type
        Gross_Profit_Margin = (gross_profit / revenue) * 100
        Operating_Profit_Margin = (operating_profit / revenue) * 100
        Net_Profit_Margin = (net_profit / revenue) * 100
        Return_on_Assets = (net_income / avg_total_assets) 
        
        # Add your calculations here
        results["Gross Profit Margin"] = Gross_Profit_Margin
        results["Operating Profit Margin"] = Operating_Profit_Margin
        results["Net Profit Margin"] = Net_Profit_Margin
        results["Return on Assets"] = Return_on_Assets

    # Add more conditions for other business types and their specific calculations
    
    elif business_type == "Trader":
        # Calculate ratios specific to the "Branding" business type
        Gross_Profit_Margin = (gross_profit / revenue) * 100
        Operating_Profit_Margin = (operating_profit / revenue) * 100
        Net_Profit_Margin = (net_profit / revenue) * 100
        Return_on_Assets = (net_income / avg_total_assets) 
        
        # Add your calculations here
        results["Gross Profit Margin"] = Gross_Profit_Margin
        results["Operating Profit Margin"] = Operating_Profit_Margin
        results["Net Profit Margin"] = Net_Profit_Margin
        results["Return on Assets"] = Return_on_Assets
        
    elif business_type == "Shipping Service":
        # Calculate ratios specific to the "Branding" business type
        Gross_Profit_Margin = (gross_profit / revenue) * 100
        Operating_Profit_Margin = (operating_profit / revenue) * 100
        Net_Profit_Margin = (net_profit / revenue) * 100
        Return_on_Assets = (net_income / avg_total_assets) 
        
        # Add your calculations here
        results["Gross Profit Margin"] = Gross_Profit_Margin
        results["Operating Profit Margin"] = Operating_Profit_Margin
        results["Net Profit Margin"] = Net_Profit_Margin
        results["Return on Assets"] = Return_on_Assets
        
    elif business_type == "Banking and Investment Services":
        
        # Calculate ratios specific to the "Branding" business type
        Gross_Profit_Margin = (gross_profit / revenue) * 100
        Operating_Profit_Margin = (operating_profit / revenue) * 100
        Net_Profit_Margin = (net_profit / revenue) * 100
        Return_on_Assets = (net_income / avg_total_assets) 
        
        # Add your calculations here
        results["Gross Profit Margin"] = Gross_Profit_Margin
        results["Operating Profit Margin"] = Operating_Profit_Margin
        results["Net Profit Margin"] = Net_Profit_Margin
        results["Return on Assets"] = Return_on_Assets
        
    elif business_type == "Software and Web Development":
        
        # Calculate ratios specific to the "Branding" business type
        Gross_Profit_Margin = (gross_profit / revenue) * 100
        Operating_Profit_Margin = (operating_profit / revenue) * 100
        Net_Profit_Margin = (net_profit / revenue) * 100
        Return_on_Assets = (net_income / avg_total_assets) 
        
        # Add your calculations here
        results["Gross Profit Margin"] = Gross_Profit_Margin
        results["Operating Profit Margin"] = Operating_Profit_Margin
        results["Net Profit Margin"] = Net_Profit_Margin
        results["Return on Assets"] = Return_on_Assets
        
    elif business_type == "Accommodation and Conference Facility":
        # Calculate ratios specific to the "Branding" business type
        Gross_Profit_Margin = (gross_profit / revenue) * 100
        Operating_Profit_Margin = (operating_profit / revenue) * 100
        Net_Profit_Margin = (net_profit / revenue) * 100
        Return_on_Assets = (net_income / avg_total_assets) 
        
        # Add your calculations here
        results["Gross Profit Margin"] = Gross_Profit_Margin
        results["Operating Profit Margin"] = Operating_Profit_Margin
        results["Net Profit Margin"] = Net_Profit_Margin
        results["Return on Assets"] = Return_on_Assets

    elif business_type == "Transportation and logistics":
        # Calculate ratios specific to the "Branding" business type
        Gross_Profit_Margin = (gross_profit / revenue) * 100
        Operating_Profit_Margin = (operating_profit / revenue) * 100
        Net_Profit_Margin = (net_profit / revenue) * 100
        Return_on_Assets = (net_income / avg_total_assets) 
        
        # Add your calculations here
        results["Gross Profit Margin"] = Gross_Profit_Margin
        results["Operating Profit Margin"] = Operating_Profit_Margin
        results["Net Profit Margin"] = Net_Profit_Margin
        results["Return on Assets"] = Return_on_Assets
        
    elif business_type == "Fuel and Pumps":
        # Calculate ratios specific to the "Branding" business type
        Gross_Profit_Margin = (gross_profit / revenue) * 100
        Operating_Profit_Margin = (operating_profit / revenue) * 100
        Net_Profit_Margin = (net_profit / revenue) * 100
        Return_on_Assets = (net_income / avg_total_assets)
        
        # Add your calculations here
        results["Gross Profit Margin"] = Gross_Profit_Margin
        results["Operating Profit Margin"] = Operating_Profit_Margin
        results["Net Profit Margin"] = Net_Profit_Margin
        results["Return on Assets"] = Return_on_Assets
        
    elif business_type == "Warehouse":
        # Calculate ratios specific to the "Branding" business type
        Gross_Profit_Margin = (gross_profit / revenue) * 100
        Operating_Profit_Margin = (operating_profit / revenue) * 100
        Net_Profit_Margin = (net_profit / revenue) * 100
        Return_on_Assets = (net_income / avg_total_assets)
        
        # Add your calculations here
        results["Gross Profit Margin"] = Gross_Profit_Margin
        results["Operating Profit Margin"] = Operating_Profit_Margin
        results["Net Profit Margin"] = Net_Profit_Margin
        results["Return on Assets"] = Return_on_Assets
    
    return results

@app.route('/', methods=['GET', 'POST'])
def upload_file():
    if request.method == 'POST':
        uploaded_file = request.files['file']
        business_type = request.form['business_type']  # Get the selected business type

        if uploaded_file.filename != '':
            file_path = 'uploads/' + uploaded_file.filename
            uploaded_file.save(file_path)

            # Calculate metrics and pass them to the template
            results = calculate_metrics(file_path, business_type)
            # print("selected ",business_type)
            # print("results here",results)
            return render_template('upload.html', business_types=business_types, selected_business=business_type, profit_margin_ranges=profit_margin_ranges, results=results)

    return render_template('upload.html', business_types=business_types)

# Your other route handling code...

if __name__ == '__main__':
    app.run(debug=True)
-->


Results.html
{% comment %} <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Financial Metrics</title>
</head>
<body>
    <h1>Financial Metrics Calculator</h1>
    
    <form method="POST" action="/" enctype="multipart/form-data">
        <label for="file">Upload a CSV file:</label>
        <input type="file" name="file" id="file" required>
        
        <label for="business_type">Select Business Type:</label>
        <select name="business_type" id="business_type" required>
            {% for business in business_types %}
                <option value="{{ business }}">{{ business }}</option>
            {% endfor %}
        </select>
        
        <input type="submit" value="Calculate">
    </form>
    
    {% if results %}
        <h2>Results for {{ selected_business }}</h2>
        <table border="1">
            <tr>
                <th>Metric</th>
                <th>Value</th>
            </tr>
            {% for metric, value in results.items() %}
                <tr>
                    <td>{{ metric }}</td>
                    <td style="color:
                        {% if metric == 'Gross Profit Margin' %}
                            {% if profit_margin_ranges[selected_business]['gross'] | replace(" and greater", "") | split(' to ') | map('float') | length == 1 and value < profit_margin_ranges[selected_business]['gross'] | replace(" and greater", "") | split(' to ') | map('float') | first %}
                                red;
                            {% elif profit_margin_ranges[selected_business]['gross'] | replace(" and greater", "") | split(' to ') | map('float') | length == 2 and (value < profit_margin_ranges[selected_business]['gross'] | replace(" and greater", "") | split(' to ') | map('float') | first or value > profit_margin_ranges[selected_business]['gross'] | replace(" and greater", "") | split(' to ') | map('float') | last) %}
                                yellow;
                            {% else %}
                                green;
                            {% endif %}
                        {% elif metric == 'Operating Profit Margin' %}
                            {% if profit_margin_ranges[selected_business]['operating'] | replace(" and greater", "") | split(' to ') | map('float') | length == 1 and value < profit_margin_ranges[selected_business]['operating'] | replace(" and greater", "") | split(' to ') | map('float') | first %}
                                red;
                            {% elif profit_margin_ranges[selected_business]['operating'] | replace(" and greater", "") | split(' to ') | map('float') | length == 2 and (value < profit_margin_ranges[selected_business]['operating'] | replace(" and greater", "") | split(' to ') | map('float') | first or value > profit_margin_ranges[selected_business]['operating'] | replace(" and greater", "") | split(' to ') | map('float') | last) %}
                                yellow;
                            {% else %}
                                green;
                            {% endif %}
                        {% elif metric == 'Net Profit Margin' %}
                            {% if profit_margin_ranges[selected_business]['net'] | replace(" and greater", "") | split(' to ') | map('float') | length == 1 and value < profit_margin_ranges[selected_business]['net'] | replace(" and greater", "") | split(' to ') | map('float') | first %}
                                red;
                            {% elif profit_margin_ranges[selected_business]['net'] | replace(" and greater", "") | split(' to ') | map('float') | length == 2 and (value < profit_margin_ranges[selected_business]['net'] | replace(" and greater", "") | split(' to ') | map('float') | first or value > profit_margin_ranges[selected_business]['net'] | replace(" and greater", "") | split(' to ') | map('float') | last) %}
                                yellow;
                            {% else %}
                                green;
                            {% endif %}
                        {% elif metric == 'Return on Assets' %}
                            {% if profit_margin_ranges[selected_business]['return'] | replace(" and greater", "") | split(' to ') | map('float') | length == 1 and value < profit_margin_ranges[selected_business]['return'] | replace(" and greater", "") | split(' to ') | map('float') | first %}
                                red;
                            {% elif profit_margin_ranges[selected_business]['return'] | replace(" and greater", "") | split(' to ') | map('float') | length == 2 and (value < profit_margin_ranges[selected_business]['return'] | replace(" and greater", "") | split(' to ') | map('float') | first or value > profit_margin_ranges[selected_business]['return'] | replace(" and greater", "") | split(' to ') | map('float') | last) %}
                                yellow;
                            {% else %}
                                green;
                            {% endif %}
                        {% endif %}
                    ">
                        {{ value }}
                    </td>
                </tr>
            {% endfor %}
        </table>
    {% endif %}
</body>
</html> {% endcomment %}


Upload.Html


<!DOCTYPE html>
<html>
<head>
    <title>Upload CSV File</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f4f4;
        }

        h1 {
            color: #333;
        }

        form {
            margin: 20px;
            padding: 20px;
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        label {
            font-weight: bold;
        }

        input[type="file"] {
            border: 1px solid #ccc;
            padding: 5px;
            margin: 5px 0;
        }

        select {
            border: 1px solid #ccc;
            padding: 5px;
            margin: 5px 0;
        }

        input[type="submit"] {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
        }

        input[type="submit"]:hover {
            background-color: #45a049;
        }

        h2 {
            color: #333;
            margin-top: 20px;
        }

        table {
            width: 80%;
            margin: 0 auto;
            border-collapse: collapse;
        }

        table, th, td {
            border: 1px solid #333;
        }

        th, td {
            padding: 10px;
            text-align: center;
        }

        th {
            background-color: #333;
            color: white;
        }

        tr:nth-child(even) {
            background-color: #f2f2f2;
        }

        td {
            background-color: #fff;
        }

        td.red {
            background-color: #FF5733;
        }

        td.yellow {
            background-color: #F7DC6F;
        }

        td.green {
            background-color: #82E0AA;
        }
    </style>
</head>
<body>
    <h1>AUTOMATE FINANCIAL ANALYSIS</h1>
    <form method="POST" action="/" enctype="multipart/form-data">
        <label for="file">Upload CSV File:</label>
        <input type="file" name="file" accept=".csv" required>
        <br>
        <label for="business_type">Select Business Type:</label>
        <select name="business_type" required>
            {% for business in business_types %}
                <option value="{{ business }}">{{ business }}</option>
            {% endfor %}
        </select>
        <br>
        <input type="submit" value="Calculate Metrics">
    </form>

    {% if selected_business %}
    <h2>Profit Margin Ranges for {{ selected_business }}</h2>
    <p><strong>Gross Profit Margin Range:</strong> {{ profit_margin_ranges[selected_business]["gross"] }}</p>
    <p><strong>Operating Profit Margin Range:</strong> {{ profit_margin_ranges[selected_business]["operating"] }}</p>
    <p><strong>Net Profit Margin Range:</strong> {{ profit_margin_ranges[selected_business]["net"] }}</p>
    <p><strong>Return on Assets Range:</strong> {{ profit_margin_ranges[selected_business]["return"] }}</p>
    {% endif %}

    {% if results %}
    <h2>Calculated Metrics</h2>
    <table border="1">
        <tr>
            <th>Metric</th>
            <th>Value</th>
            <th>Color</th>
        </tr>
        <tr>
            <td>Gross Profit Margin</td>
            <td>{{ results["Gross Profit Margin"] }}%</td>
            <td class="{% if results["Gross Profit Margin"] < 20 %}red{% elif results["Gross Profit Margin"] >= 20 and results["Gross Profit Margin"] <= 40 %}yellow{% else %}green{% endif %}"></td>
        </tr>
        <tr>
            <td>Operating Profit Margin</td>
            <td>{{ results["Operating Profit Margin"] }}%</td>
            <td class="{% if results["Operating Profit Margin"] < 10 %}red{% elif results["Operating Profit Margin"] >= 10 and results["Operating Profit Margin"] <= 20 %}yellow{% else %}green{% endif %}"></td>
        </tr>
        <tr>
            <td>Net Profit Margin</td>
            <td>{{ results["Net Profit Margin"] }}%</td>
            <td class="{% if results["Net Profit Margin"] < 5 %}red{% elif results["Net Profit Margin"] >= 5 and results["Net Profit Margin"] <= 15 %}yellow{% else %}green{% endif %}"></td>
        </tr>
        <tr>
            <td>Return on Assets</td>
            <td>{{ results["Return on Assets"] }}%</td>
            <td class="{% if results["Return on Assets"] < 5 %}red{% elif results["Return on Assets"] >= 5 and results["Return on Assets"] <= 15 %}yellow{% else %}green{% endif %}"></td>
        </tr>
    </table>
    {% endif %}
</body>
</html>




