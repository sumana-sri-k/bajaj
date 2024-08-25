pip install Flask
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/bfhl', methods=['POST'])
def handle_post():
    try:
        data = request.json.get('data', [])
        user_id = "john_doe_17091999"  # Replace with your logic
        email = "john@xyz.com"
        roll_number = "ABCD123"
        numbers = [item for item in data if item.isdigit()]
        alphabets = [item for item in data if item.isalpha()]
        lowercase_alphabets = [item for item in alphabets if item.islower()]
        highest_lowercase = max(lowercase_alphabets) if lowercase_alphabets else None
        response = {
            "is_success": True,
            "user_id": user_id,
            "email": email,
            "roll_number": roll_number,
            "numbers": numbers,
            "alphabets": alphabets,
            "highest_lowercase_alphabet": [highest_lowercase] if highest_lowercase else []
        }
        return jsonify(response), 20
       except Exception as e:
        return jsonify({"is_success": False, "error": str(e)}), 400

@app.route('/bfhl', methods=['GET'])
def handle_get():
    return jsonify({"operation_code": 1}), 200

if __name__ == '__main__':
    app.run(debug=True)
