from pywebio import start_server
from pywebio.input import input, input_group, NUMBER
from pywebio.output import put_markdown, put_table, put_text, put_success, put_warning, put_html, clear

def calculate_bmi(height_cm, weight_kg):
    height_m = height_cm / 100
    bmi = weight_kg / (height_m ** 2)
    return round(bmi, 2)

def get_bmi_status(bmi):
    if bmi < 18.5:
        return "Underweight", "warning"
    elif 18.5 <= bmi < 24.9:
        return "Normal weight", "success"
    elif 25.0 <= bmi < 29.9:
        return "Overweight", "warning"
    else:
        return "Obese", "danger"

def health_dashboard():
    put_markdown("# 🏋️‍♂️ Personal Health & BMI Dashboard")
    put_markdown("Welcome to the BMI Calculator!")
    put_html("<hr>") 

    while True:
       
        user_data = input_group("Please enter your metrics:", [
            input("Enter your Name:", name="user_name", required=True),
            input("Enter Height (in cm):", name="height", type=NUMBER, required=True),
            input("Enter Weight (in kg):", name="weight", type=NUMBER, required=True)])
        
        name = user_data["user_name"]
        height = user_data["height"]
        weight = user_data["weight"]
        
        bmi_value = calculate_bmi(height, weight)
        status, alert_type = get_bmi_status(bmi_value)
        
        clear()
        
        put_markdown(f"## 📊 Results for {name}")
        
        put_table([
            ['Metric', 'Your Value'],
            ['Height', f"{height} cm"],
            ['Weight', f"{weight} kg"],
            ['Calculated BMI', f"{bmi_value}"]])
        
       
        if alert_type == "success":
            put_success(f"Congratulations {name}! Your BMI is {bmi_value} ({status}). Keep up the great lifestyle!")
        else:
            put_warning(f"Notice: Your BMI is {bmi_value} ({status}). Consider consulting a health professional if needed.")
            
        put_markdown("""
        ### 📌 BMI Reference Range Reference:
        * **Underweight:** Below 18.5
        * **Normal weight:** 18.5 – 24.9
        * **Overweight:** 25.0 – 29.9
        * **Obese:** 30.0 or higher
        """)
        
        put_html("<br>")
        input("Press 'Submit' to calculate for another person", button_text="Restart Calculator")
        clear()

if __name__ == '__main__':
    start_server(health_dashboard, port=8080, debug=True)
