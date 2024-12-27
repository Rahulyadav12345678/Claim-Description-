<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blockchain Claim System</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f7f6;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 20px;
        }

        form {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 500px;
        }

        label {
            font-size: 16px;
            color: #555;
            margin-bottom: 8px;
            display: inline-block;
        }

        textarea, input[type="number"] {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 14px;
            box-sizing: border-box;
        }

        textarea {
            height: 150px;
            resize: none;
        }

        button {
            background-color: #4CAF50;
            color: white;
            font-size: 16px;
            padding: 12px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            width: 100%;
        }

        button:hover {
            background-color: #45a049;
        }

        #status {
            margin-top: 20px;
            text-align: center;
            font-size: 18px;
        }

        .error {
            color: red;
        }

        .success {
            color: green;
        }
    </style>
</head>
<body>
    <div>
        <h1>Submit Claim</h1>

        <form id="claim-form">
            <label for="description">Claim Description:</label>
            <textarea id="description" required></textarea>

            <label for="amount">Claim Amount:</label>
            <input type="number" id="amount" required>

            <button type="submit">Submit Claim</button>
        </form>

        <div id="status"></div>
    </div>

    <script>
        document.getElementById('claim-form').addEventListener('submit', async function(event) {
            event.preventDefault();

            const description = document.getElementById('description').value;
            const amount = document.getElementById('amount').value;

            const fromAddress = '0xYourMetaMaskAddress'; // Replace with the address from MetaMask

            const response = await fetch('http://localhost:3000/submit-claim', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    description,
                    amount,
                    fromAddress
                })
            });

            const data = await response.json();
            const statusDiv = document.getElementById('status');

            if (data.message) {
                statusDiv.innerText = data.message;
                statusDiv.classList.remove('error');
                statusDiv.classList.add('success');
            } else {
                statusDiv.innerText = data.error || 'An unknown error occurred.';
                statusDiv.classList.remove('success');
                statusDiv.classList.add('error');
            }
        });
    </script>
</body>
</html>
