# early-detect-DR-AI
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>CareTriage AI</title>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
}

body {
    background: #f4f7fb;
    color: #222;
}

header {
    background: #123b6d;
    color: white;
    text-align: center;
    padding: 30px 15px;
}

header h1 {
    font-size: 32px;
    margin-bottom: 8px;
}

header p {
    font-size: 16px;
}

.container {
    width: 90%;
    max-width: 900px;
    margin: 30px auto;
}

.card, .result-card {
    background: white;
    padding: 25px;
    margin-bottom: 25px;
    border-radius: 12px;
    box-shadow: 0 3px 12px rgba(0,0,0,0.1);
}

h2 {
    margin-bottom: 20px;
    color: #123b6d;
}

label {
    display: block;
    margin-top: 15px;
    font-weight: bold;
}

input[type="text"],
input[type="number"] {
    width: 100%;
    padding: 12px;
    margin-top: 7px;
    border: 1px solid #ccc;
    border-radius: 7px;
}

.symptoms {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
    margin-top: 10px;
}

.symptoms label {
    background: #f1f5f9;
    padding: 12px;
    border-radius: 7px;
    font-weight: normal;
}

button {
    width: 100%;
    margin-top: 25px;
    padding: 14px;
    background: #1976d2;
    color: white;
    border: none;
    border-radius: 7px;
    font-size: 17px;
    cursor: pointer;
}

button:hover {
    background: #0d5ca8;
}

.result-card {
    border-left: 6px solid #1976d2;
}

.result {
    padding: 15px;
    border-radius: 8px;
    margin-top: 10px;
}

.urgent {
    background: #ffe1e1;
    color: #a00000;
}

.priority {
    background: #fff0cc;
    color: #8a5a00;
}

.routine {
    background: #ddf5e3;
    color: #176b2c;
}

footer {
    text-align: center;
    padding: 25px;
    color: #666;
    font-size: 13px;
}

@media (max-width: 600px) {
    .symptoms {
        grid-template-columns: 1fr;
    }
}
</style>
</head>

<body>

<header>
    <h1>CareTriage AI</h1>
    <p>AI-Assisted Triage Support for Primary Health Centres</p>
</header>

<div class="container">

    <section class="card">

        <h2>Patient Information</h2>

        <label>Patient Name</label>
        <input type="text" id="name" placeholder="Enter patient name">

        <label>Age</label>
        <input type="number" id="age" placeholder="Enter age">

        <label>Select Symptoms</label>

        <div class="symptoms">

            <label>
                <input type="checkbox" value="fever">
                Fever
            </label>

            <label>
                <input type="checkbox" value="breathing">
                Difficulty in Breathing
            </label>

            <label>
                <input type="checkbox" value="chest">
                Chest Pain
            </label>

            <label>
                <input type="checkbox" value="headache">
                Severe Headache
            </label>

            <label>
                <input type="checkbox" value="vomiting">
                Vomiting
            </label>

            <label>
                <input type="checkbox" value="weakness">
                Weakness
            </label>

        </div>

        <button onclick="analyzePatient()">
            Analyze Triage
        </button>

    </section>


    <section class="result-card" id="result">

        <h2>Triage Result</h2>

        <p>
            Enter patient details and symptoms to generate a result.
        </p>

    </section>

</div>


<footer>

    <p>CareTriage AI | Omnikon Hackathon 2026</p>

    <p>
        This is a prototype for decision-support demonstration
        and is not a medical diagnosis system.
    </p>

</footer>


<script>

function analyzePatient() {

    const name = document.getElementById("name").value;
    const age = document.getElementById("age").value;

    const selectedSymptoms = [];

    document.querySelectorAll(
        '.symptoms input[type="checkbox"]:checked'
    ).forEach(function(checkbox) {

        selectedSymptoms.push(checkbox.value);

    });


    if (name === "" || age === "") {

        alert("Please enter patient name and age.");

        return;
    }


    if (selectedSymptoms.length === 0) {

        alert("Please select at least one symptom.");

        return;
    }


    /*
       Prototype triage-support logic.
       This does NOT provide medical diagnosis.
    */

    const urgentSymptoms = [
        "breathing",
        "chest"
    ];


    let urgent = false;


    selectedSymptoms.forEach(function(symptom) {

        if (urgentSymptoms.includes(symptom)) {

            urgent = true;

        }

    });


    let category;
    let explanation;
    let className;


    if (urgent) {

        category = "URGENT";

        className = "urgent";

        explanation =
            "Potential warning symptoms were selected. " +
            "The patient should receive prompt assessment " +
            "by a qualified healthcare professional.";

    }

    else if (selectedSymptoms.length >= 3) {

        category = "PRIORITY";

        className = "priority";

        explanation =
            "Multiple symptoms were reported. " +
            "The patient should be reviewed by healthcare staff " +
            "according to local clinical protocols.";

    }

    else {

        category = "ROUTINE";

        className = "routine";

        explanation =
            "No prototype-defined urgent warning symptom was selected. " +
            "Continue with normal clinical assessment and local triage procedures.";

    }


    document.getElementById("result").innerHTML = `

        <h2>Triage Result</h2>

        <div class="result ${className}">

            <h3>${category}</h3>

            <p>
                <strong>Patient:</strong> ${name}
            </p>

            <p>
                <strong>Age:</strong> ${age}
            </p>

            <p>
                <strong>Symptoms:</strong>
                ${selectedSymptoms.join(", ")}
            </p>

            <br>

            <p>
                <strong>Explanation:</strong>
            </p>

            <p>
                ${explanation}
            </p>

        </div>

        <p style="margin-top:15px; font-size:13px;">

            ⚠️ This is a hackathon prototype for
            decision-support workflow demonstration.
            It does not provide medical diagnosis or treatment.

        </p>

    `;

}

</script>

</body>
</html>
