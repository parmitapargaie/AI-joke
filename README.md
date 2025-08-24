# AI-joke <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>AI Joke Teller</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f9f9f9;
      text-align: center;
      margin-top: 40px;
    }
    h1 {
      color: #222;
    }
    #jokeBox {
      margin: 20px auto;
      padding: 20px;
      max-width: 700px;
      background: white;
      border-radius: 12px;
      box-shadow: 0px 4px 6px rgba(0,0,0,0.1);
      font-size: 1.2em;
      min-height: 100px;
    }
    .btn-container {
      margin-top: 20px;
    }
    button {
      padding: 10px 18px;
      font-size: 1em;
      border: none;
      border-radius: 8px;
      margin: 5px;
      cursor: pointer;
      transition: 0.3s;
      color: white;
    }
    button:hover {
      opacity: 0.8;
    }
    .funny { background-color: #f39c12; }
    .happy { background-color: #27ae60; }
    .sad   { background-color: #3498db; }
    .tech  { background-color: #9b59b6; }
    .school{ background-color: #e74c3c; }
  </style>
</head>
<body>
  <h1>😂 AI Joke Teller 😂</h1>
  <div id="jokeBox">Click a mood button to hear a joke!</div>

  <div class="btn-container">
    <button class="funny" onclick="tellJoke('funny')">Funny</button>
    <button class="happy" onclick="tellJoke('happy')">Happy</button>
    <button class="sad" onclick="tellJoke('sad')">Sad</button>
    <button class="tech" onclick="tellJoke('tech')">Tech</button>
    <button class="school" onclick="tellJoke('school')">School</button>
  </div>

  <script>
    // Joke database by category (20 each)
    const jokes = {
      funny: [
        "Why don’t scientists trust atoms? Because they make up everything!",
        "Why can’t your nose be 12 inches long? Because then it would be a foot!",
        "Why don’t skeletons fight each other? They don’t have the guts.",
        "I only know 25 letters of the alphabet. I don’t know y.",
        "Why did the scarecrow win an award? Because he was outstanding in his field.",
        "Why don’t oysters donate to charity? Because they’re shellfish.",
        "Why did the tomato blush? Because it saw the salad dressing!",
        "Why don’t eggs tell jokes? They’d crack each other up.",
        "Why was the computer cold? It left its Windows open.",
        "I told my wife she should embrace her mistakes. She hugged me.",
        "Why don’t cows have money? Because farmers milk them dry.",
        "Why did the bike fall over? It was two-tired.",
        "Why can’t your nose be 30 cm long? Because then it would be a ruler.",
        "Why don’t seagulls fly over the bay? Because then they’d be bagels.",
        "Why did the math book look sad? It had too many problems.",
        "Why don’t frogs play basketball? They’re afraid of the net.",
        "Why can’t you trust stairs? They’re always up to something.",
        "Why was the broom late? It overswept.",
        "Why don’t ants get sick? Because they have tiny ant-bodies.",
        "Why did the golfer bring an extra pair of pants? In case he got a hole in one."
      ],
      happy: [
        "What kind of tree fits in your hand? A palm tree!",
        "Why did the golfer bring two pairs of pants? In case he got a hole in one.",
        "Why was the math book smiling? Because it solved all its problems!",
        "Why don’t bees ever get married? Because they’re busy bees.",
        "Why did the cookie go to the doctor? Because it was feeling crummy.",
        "Why did the banana go to the party? Because it was a-peeling.",
        "Why was the broom so happy? Because it swept someone off their feet.",
        "Why did the chicken join a band? Because it had drumsticks.",
        "Why did the cow win an award? Because it was udderly amazing.",
        "Why was the sun so happy? It finally found its ray of sunshine.",
        "Why did the boy bring a ladder to school? To reach high grades.",
        "Why was the calendar always happy? Because its days were numbered in joy.",
        "Why was the pencil smiling? Because it finally got the point.",
        "Why was the music teacher happy? Because her students were in harmony.",
        "Why did the balloon go to the party? Because it was full of hot air.",
        "Why was the lightbulb so bright? Because it was switched on to happiness.",
        "Why did the toy laugh? Because it was tickled pink.",
        "Why was the cat so cheerful? Because it was feline fine.",
        "Why did the flower always smile? Because it bloomed with joy.",
        "Why was the math teacher so happy? Because her problems were finally solved."
      ],
      sad: [
        "Parallel lines have so much in common… it’s a shame they’ll never meet.",
        "I told my computer I needed a break, and now it won’t stop sending me Kit-Kats.",
        "Why did the scarecrow break up? It felt empty inside.",
        "I used to play piano by ear, but now I use my hands.",
        "My dog used to chase people on a bike… it got too tired.",
        "I lost my mood ring. I don’t know how I feel about it.",
        "I was going to tell a time-travel joke, but you didn’t like it.",
        "I’d tell you a chemistry joke, but I know I wouldn’t get a reaction.",
        "Why was the skeleton lonely? Because no body liked him.",
        "I asked the librarian if the library had books on paranoia. She whispered, 'They’re right behind you.'",
        "Why did the candle go to therapy? It was burned out.",
        "My computer crashed, so I gave it a pillow.",
        "Why was the belt arrested? For holding up a pair of pants.",
        "I was wondering why the ball kept getting bigger… then it hit me.",
        "I used to be a baker, but I couldn’t make enough dough.",
        "I told my wife she should embrace her flaws… she gave me a hug.",
        "Why did the phone cry? It lost its contacts.",
        "I was going to tell a joke about depression, but it never cheered up.",
        "Why did the student eat his homework? Because his teacher said it was a piece of cake.",
        "I told my shadow I was sad, but it just followed me silently."
      ],
      tech: [
        "Why do Java developers wear glasses? Because they don’t C#.",
        "There are 10 types of people in the world: those who understand binary, and those who don’t.",
        "Why was the computer cold? It forgot to close its Windows.",
        "Why do programmers prefer dark mode? Because light attracts bugs.",
        "Why did the smartphone go to therapy? It lost its sense of touch.",
        "Why was the computer tired when it got home? It had too many tabs open.",
        "Why did the programmer quit his job? Because he didn’t get arrays.",
        "Why was the robot angry? People kept pushing its buttons.",
        "Why do hackers wear hoodies? To hide in the code shadows.",
        "Why did the AI cross the road? To optimize the chicken’s path.",
        "Why was the computer sneezing? It had a virus.",
        "Why don’t computers play hide and seek? Because they always get cached.",
        "Why was the tech book sad? Too many errors.",
        "Why was the Wi-Fi so moody? Because it kept losing connection.",
        "Why was the server stressed? Too many requests.",
        "Why did the coder bring a ladder? To reach higher-level languages.",
        "Why do coders like jokes about recursion? Because they can repeat them forever.",
        "Why was the keyboard excited? Because it found its type.",
        "Why do computers love snacks? Because they love bytes.",
        "Why was the mouse happy? Because it clicked with everyone."
      ],
      school: [
        "Teacher: 'Why are you late?' Student: 'Because of the sign.' Teacher: 'What sign?' Student: 'School Ahead, Go Slow!'",
        "Why was the math book sad? Because it had too many problems!",
        "Why did the student eat his homework? Because the teacher said it was a piece of cake.",
        "Why did the teacher wear sunglasses? Because her students were so bright.",
        "Why did the boy bring a ladder to school? To reach high grades.",
        "Why was the teacher cross-eyed? She couldn’t control her pupils.",
        "Why did the music teacher go to the principal? Because she found herself in treble.",
        "Why did the student bring a pencil to the party? To draw attention.",
        "Why was the history teacher always tired? Too many dates.",
        "Why did the student do multiplication on the floor? Because the teacher told him not to use tables.",
        "Why did the English teacher go to the beach? To test the water.",
        "Why did the student bring string to school? To tie up loose ends.",
        "Why was the math class so noisy? Because of all the functions.",
        "Why did the student bring scissors to school? To cut class.",
        "Why did the teacher wear glasses? To improve her pupils’ focus.",
        "Why did the geography book look so depressed? Too many maps.",
        "Why did the student bring a flashlight? To go through a dark chapter.",
        "Why did the principal go to the bank? To check his balance.",
        "Why did the student bring a ruler to school? To measure up.",
        "Why was the science teacher at the beach? To test the waves."
      ]
    };

    function tellJoke(category) {
      const selectedJokes = jokes[category];
      const randomIndex = Math.floor(Math.random() * selectedJokes.length);
      document.getElementById("jokeBox").innerText = selectedJokes[randomIndex];
    }
  </script>
</body>
</html>
