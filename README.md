<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gifts of the Spirit Test</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 20px;
            max-width: 800px;
            margin: auto;
        }
        .question {
            margin-bottom: 15px;
        }
        .scale {
            display: flex;
            gap: 10px;
            align-items: center;
        }
        .scale label {
            cursor: pointer;
            padding: 5px 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            background: #f8f8f8;
            transition: 0.2s;
        }
        .scale input {
            display: none;
        }
        .scale input:checked + label {
            background: #4CAF50;
            color: white;
            font-weight: bold;
            border-color: #4CAF50;
        }
        .results {
            margin-top: 20px;
            display: none;
        }
        .rating-header {
            font-weight: bold;
            margin-bottom: 10px;
        }
        #submitBtn.clicked {
            background-color: #4CAF50;
            color: white;
            border: none;
        }
    </style>
</head>
<body>
    <h2>Gifts of the Spirit Test</h2>
    <p class="rating-header">Rate each statement from 1 to 5 (1 = Lowest, 5 = Highest):</p>
    
    <form id="quizForm">
        <div id="questionsContainer"></div>
        <button type="button" id="submitBtn">Submit</button>
    </form>
    
    <div class="results" id="results">
        <h3>Your Top 5 Spiritual Gifts:</h3>
        <ul id="resultsList"></ul>
    </div>
    
    <script>
        document.addEventListener("DOMContentLoaded", function () {
            const questions = [
                  { code: "Q56", gift: "Word of Knowledge", text: "I often recognize biblical patterns and themes others overlook." }, 
{ code: "Q92", gift: "Discernment", text: "I often discern when someone’s teachings are false or misleading." }, 
{ code: "Q40", gift: "Mercy", text: "I am willing to help people even when they have nothing to offer in return." }, 
{ code: "Q72", gift: "Healing", text: "When I pray for healing, I have a deep sense of faith that it will happen." }, 
{ code: "Q115", gift: "Evangelism", text: "I am comfortable sharing my faith with strangers or people from different backgrounds." }, 
{ code: "Q27", gift: "Leadership", text: "I naturally take charge when I see something that needs direction." }, 
{ code: "Q88", gift: "Working of Miracles", text: "People often tell me they are amazed by how God moves when I pray." }, 
{ code: "Q7", gift: "Ministering", text: "I prefer actions over words when showing love to others." }, 
{ code: "Q52", gift: "Word of Knowledge", text: "People often ask me to clarify difficult biblical passages." }, 
{ code: "Q134", gift: "Prophecy", text: "I sometimes feel a strong urgency to warn people about their spiritual condition." }, 
{ code: "Q18", gift: "Exhortation", text: "People often tell me that my words have given them new hope." }, 
{ code: "Q108", gift: "Administration", text: "People trust me to manage important responsibilities." }, 
{ code: "Q64", gift: "Faith", text: "I am unwavering in my trust in God’s promises." }, 
{ code: "Q98", gift: "Interpretation of Tongues", text: "I have had moments where I instinctively understood words spoken in tongues." }, 
{ code: "Q126", gift: "Generosity", text: "I have often given beyond what was expected, knowing God would take care of me." }, 
{ code: "Q3", gift: "Ministering", text: "I feel fulfilled when I assist others in their calling, even if I receive no recognition." }, 
{ code: "Q50", gift: "Word of Knowledge", text: "I naturally connect biblical knowledge with real-life applications." }, 
{ code: "Q110", gift: "Administration", text: "I enjoy creating order out of chaos." }, 
{ code: "Q132", gift: "Prophecy", text: "People have told me that my words are direct but necessary." }, 
{ code: "Q21", gift: "Exhortation", text: "I often share Scripture or testimonies to inspire others." }, { code: "Q43", gift: "Word of Wisdom", text: "People seek my advice because they say it is wise and insightful." }, 
{ code: "Q65", gift: "Healing", text: "I often feel led to pray for people's healing." }, 
{ code: "Q16", gift: "Teaching", text: "I am passionate about sharing knowledge that can help others grow spiritually." }, 
{ code: "Q80", gift: "Speaking in Tongues", text: "I desire to grow in my ability to pray in the Spirit more fluently." }, 
{ code: "Q128", gift: "Generosity", text: "I believe generosity is a way of expressing God's love." }, 
{ code: "Q104", gift: "Interpretation of Tongues", text: "I believe that understanding tongues brings clarity and encouragement to the church." }, 
{ code: "Q48", gift: "Word of Wisdom", text: "I often experience moments of sudden spiritual insight." }, 
{ code: "Q31", gift: "Leadership", text: "People respect my ability to make difficult decisions with clarity." }, 
{ code: "Q87", gift: "Working of Miracles", text: "I have sensed God prompting me to ask for miracles beyond my expectations." }, 
{ code: "Q117", gift: "Evangelism", text: "I believe leading others to Christ is one of my greatest joys." }, 
{ code: "Q90", gift: "Discernment", text: "I can often tell if something is spiritually good or evil before others recognize it." }, 
{ code: "Q70", gift: "Healing", text: "I believe divine healing is part of God's will for His people." }, { code: "Q14", gift: "Teaching", text: "I am drawn to discussions where I can clarify misunderstandings." }, 
{ code: "Q58", gift: "Faith", text: "I believe in God’s provision even when circumstances seem hopeless." }, 
{ code: "Q106", gift: "Administration", text: "I enjoy handling details that help ministries or events run effectively." }, 
{ code: "Q123", gift: "Generosity", text: "I look for opportunities to support ministries, missions, or those in need." }, 
{ code: "Q141", gift: "Prophecy", text: "I believe God has given me insight into what He wants His people to hear." }, 
{ code: "Q25", gift: "Leadership", text: "I feel a strong sense of responsibility to guide and direct people." },
{ code: "Q120", gift: "Evangelism", text: "I rejoice deeply when I see someone accept Christ." }, 
{ code: "Q77", gift: "Speaking in Tongues", text: "Others have confirmed that my prayers in tongues have encouraged them." }, 
{ code: "Q35", gift: "Mercy", text: "I feel a strong urge to comfort those who are struggling emotionally." }, 
{ code: "Q47", gift: "Word of Wisdom", text: "I have made decisions that later proved to be incredibly wise." }, 
{ code: "Q142", gift: "Prophecy", text: "I desire to see people align their lives with biblical truth." }, 
{ code: "Q96", gift: "Discernment", text: "I have received insight about people’s spiritual struggles without them telling me." }, 
{ code: "Q19", gift: "Exhortation", text: "I naturally see potential in people and encourage them to reach it." }, 
{ code: "Q76", gift: "Speaking in Tongues", text: "I have a strong desire to pray in the Spirit during worship or intercession." }, 
{ code: "Q12", gift: "Teaching", text: "I feel excited when I help someone understand a new concept." }, 
{ code: "Q133", gift: "Prophecy", text: "I have felt prompted to speak God’s truth even when it was unpopular." }, 
{ code: "Q30", gift: "Leadership", text: "I enjoy inspiring and directing groups to accomplish big-picture goals." }, 
{ code: "Q60", gift: "Faith", text: "I feel a deep confidence in God’s power beyond human understanding." }, 
{ code: "Q79", gift: "Speaking in Tongues", text: "I feel a powerful spiritual release when I pray in tongues." }, 
{ code: "Q127", gift: "Generosity", text: "I feel a special prompting to give when I see a financial or material need." }, 
{ code: "Q34", gift: "Mercy", text: "I am naturally drawn to people who are suffering or marginalized." }, 
{ code: "Q73", gift: "Speaking in Tongues", text: "I have prayed in a language I did not understand." },
    { code: "Q93", gift: "Discernment", text: "I feel a strong awareness of the spiritual atmosphere in a room." },
    { code: "Q5", gift: "Ministering", text: "I feel energized when serving, even if it requires personal sacrifice." },
    { code: "Q51", gift: "Word of Knowledge", text: "I enjoy deep study and research of biblical and theological topics." },
    { code: "Q99", gift: "Interpretation of Tongues", text: "I believe God can use me to help interpret messages given in tongues." },
    { code: "Q114", gift: "Evangelism", text: "I feel a burden for people who have never heard about Jesus." },
    { code: "Q38", gift: "Mercy", text: "I am patient with people even when they make repeated mistakes." },
    { code: "Q105", gift: "Administration", text: "I naturally organize and structure tasks to ensure smooth operations." },
    { code: "Q46", gift: "Word of Wisdom", text: "I sometimes sense when people are struggling before they say anything." },
    { code: "Q22", gift: "Exhortation", text: "I feel a strong burden to motivate people toward spiritual growth." },
    { code: "Q67", gift: "Healing", text: "I believe God still heals today and expect it when I pray." },
    { code: "Q36", gift: "Mercy", text: "I often sense what others are feeling before they express it." },
    { code: "Q86", gift: "Working of Miracles", text: "I feel compelled to pray for divine breakthroughs in difficult situations." },
    { code: "Q118", gift: "Evangelism", text: "I feel a sense of urgency to reach lost people before it is too late." },
    { code: "Q55", gift: "Word of Knowledge", text: "I love learning new things from Scripture and explaining them to others." },
    { code: "Q13", gift: "Teaching", text: "I naturally research, analyze, and study information to gain deeper insight." },
    { code: "Q109", gift: "Administration", text: "I thrive in administrative roles where I can plan and execute tasks." },
    { code: "Q44", gift: "Word of Wisdom", text: "I have a deep understanding of spiritual truths that others find challenging." },
    { code: "Q17", gift: "Exhortation", text: "I feel compelled to encourage and uplift others, especially in difficult times." },
    { code: "Q8", gift: "Ministering", text: "I feel deep satisfaction knowing I’ve helped others accomplish their goals." },
    { code: "Q28", gift: "Leadership", text: "Others often look to me for guidance in decision-making." },
    { code: "Q20", gift: "Exhortation", text: "I find great joy in reassuring others of God’s promises." },
    { code: "Q95", gift: "Discernment", text: "People have told me that my spiritual discernment has helped them." },
    { code: "Q53", gift: "Word of Knowledge", text: "I can discern biblical principles in various life situations." },
    { code: "Q59", gift: "Faith", text: "People often tell me that my faith encourages them to trust God more." },
    { code: "Q42", gift: "Word of Wisdom", text: "I find myself offering solutions that others say are profound." },
    { code: "Q85", gift: "Working of Miracles", text: "I expect God to show His power in extraordinary ways." },
    { code: "Q11", gift: "Teaching", text: "People often seek me out for explanations of biblical topics." },
    { code: "Q125", gift: "Generosity", text: "I trust God to provide for me so that I can continue being generous." },
    { code: "Q4", gift: "Ministering", text: "I often anticipate others' needs and meet them before they ask." },
    { code: "Q29", gift: "Leadership", text: "I feel a strong sense of vision for the future and desire to lead others toward it." },
    { code: "Q68", gift: "Healing", text: "People come to me for prayer when they are sick." },
    { code: "Q102", gift: "Interpretation of Tongues", text: "I have been able to confirm an interpretation of tongues spoken by others." },
    { code: "Q122", gift: "Generosity", text: "I believe God blesses me so that I can give generously." },
    { code: "Q78", gift: "Speaking in Tongues", text: "I believe speaking in tongues is a way to strengthen my faith." },
    { code: "Q32", gift: "Leadership", text: "I thrive in environments where I can cast vision and rally people toward it." },
    { code: "Q101", gift: "Interpretation of Tongues", text: "I feel that interpreting tongues helps strengthen the body of Christ." },
    { code: "Q26", gift: "Leadership", text: "I enjoy organizing and mobilizing people toward a common goal." },
    { code: "Q116", gift: "Evangelism", text: "I actively seek opportunities to talk about Jesus with others." },
    { code: "Q37", gift: "Mercy", text: "I believe showing kindness is just as important as telling the truth." },
    { code: "Q39", gift: "Mercy", text: "I am quick to offer forgiveness when others fail or hurt me." },
    { code: "Q66", gift: "Healing", text: "I have seen people recover after I prayed for them." },
    { code: "Q140", gift: "Prophecy", text: "I sense a responsibility to challenge and correct false beliefs." },
    { code: "Q112", gift: "Administration", text: "I take joy in ensuring that behind-the-scenes details are handled properly." },
    { code: "Q74", gift: "Speaking in Tongues", text: "When I pray, I sometimes feel the Holy Spirit speaking through me in a special way." },
    { code: "Q15", gift: "Teaching", text: "I enjoy developing structured lessons or presentations." },
    { code: "Q23", gift: "Exhortation", text: "When people feel discouraged, I am quick to remind them of God's faithfulness." },
    { code: "Q49", gift: "Word of Knowledge", text: "I am able to recall and apply Scripture easily to different situations." },
    { code: "Q141", gift: "Prophecy", text: "I believe God has given me insight into what He wants His people to hear." },
    { code: "Q61", gift: "Faith", text: "I am not easily discouraged because I know God is in control." },
    { code: "Q91", gift: "Discernment", text: "I have sensed when a person is lying or hiding something important." },
    { code: "Q121", gift: "Generosity", text: "I enjoy giving financially or materially to help others." },
    { code: "Q100", gift: "Interpretation of Tongues", text: "I have sensed a clear interpretation when someone prayed in tongues." },
    { code: "Q45", gift: "Word of Wisdom", text: "I feel led to provide counsel that seems beyond my own natural understanding." },
    { code: "Q9", gift: "Teaching", text: "I enjoy discovering and sharing deep truths from Scripture." },
    { code: "Q130", gift: "Prophecy", text: "I feel strongly called to declare God’s truth boldly." },
    { code: "Q62", gift: "Faith", text: "I believe God can do miracles today just as He did in the Bible." },
    { code: "Q24", gift: "Exhortation", text: "I look for ways to build confidence in others through positive words." },
    { code: "Q54", gift: "Word of Knowledge", text: "I feel compelled to share truths I’ve learned with others." },
    { code: "Q97", gift: "Interpretation of Tongues", text: "I have received a sudden understanding of the meaning of a spoken tongue." },
    { code: "Q6", gift: "Ministering", text: "I find joy in relieving others’ burdens, even with mundane tasks." },
    { code: "Q89", gift: "Discernment", text: "I have an inner knowing about people or situations that is later confirmed." },
    { code: "Q129", gift: "Prophecy", text: "I feel strongly called to declare God’s truth boldly." },
    { code: "Q113", gift: "Evangelism", text: "I have a deep desire to share the Gospel with those who don’t know Christ." },
    { code: "Q10", gift: "Teaching", text: "I often explain complex ideas in ways that others understand easily." },
    { code: "Q57", gift: "Faith", text: "I find it easy to trust God in impossible situations." },
    { code: "Q84", gift: "Working of Miracles", text: "I have prayed for supernatural intervention and seen it occur." },
    { code: "Q131", gift: "Prophecy", text: "I feel led to share messages that bring conviction and repentance." },
    { code: "Q137", gift: "Working of Miracles", text: "I have experienced or witnessed supernatural occurrences that cannot be explained naturally." },
    { code: "Q138", gift: "Evangelism", text: "I feel a strong desire to reach those who do not know Christ, regardless of the challenges." },
    { code: "Q139", gift: "Discernment", text: "I can sense when something is spiritually harmful before it becomes evident to others." },
    { code: "Q140", gift: "Leadership", text: "I have a natural ability to guide and influence people toward a shared vision." },
    { code: "Q166", gift: "Word of Wisdom", text: "I can see the long-term consequences of decisions before others recognize them." },
    { code: "Q142", gift: "Teaching", text: "I am passionate about helping people grow in their knowledge of Scripture." },
    { code: "Q143", gift: "Healing", text: "I have witnessed or experienced physical healing as a result of prayer." },
    { code: "Q144", gift: "Administration", text: "I am highly organized and able to coordinate complex projects effectively." },
    { code: "Q145", gift: "Generosity", text: "I find great joy in giving to others, even when it requires personal sacrifice." },
    { code: "Q146", gift: "Speaking in Tongues", text: "I have spoken in tongues and felt a deep spiritual connection through it." },
    { code: "Q147", gift: "Interpretation of Tongues", text: "I have been able to understand or interpret messages spoken in tongues." },
    { code: "Q148", gift: "Exhortation", text: "I enjoy motivating people to pursue their God-given potential." },
    { code: "Q149", gift: "Mercy", text: "I feel a deep sense of compassion for those who are hurting and am quick to respond." },
    { code: "Q150", gift: "Faith", text: "I believe God will provide even when circumstances seem impossible." },
    { code: "Q151", gift: "Prophecy", text: "I feel a strong urge to speak truth, even when it is unpopular or difficult." }
];

            const container = document.getElementById("questionsContainer");

            // ✅ Generate questions dynamically
            questions.forEach((q, index) => {
                const div = document.createElement("div");
                div.classList.add("question");
                div.innerHTML = `
                    <p>${index + 1}. ${q.text}</p>
                    <div class="scale">
                        ${[1, 2, 3, 4, 5].map(num => `
                            <label for="${q.code}-${num}">
                                <input type="radio" id="${q.code}-${num}" name="${q.code}" value="${num}" data-gift="${q.gift}">
                                ${num}
                            </label>
                        `).join('')}
                    </div>
                `;
                container.appendChild(div);
            });

            document.querySelectorAll(".scale input").forEach(input => {
                input.addEventListener("change", function() {
                    let scaleDiv = this.closest(".scale");
                    if (!scaleDiv) return;

                    let labels = scaleDiv.querySelectorAll("label");
                    labels.forEach(label => label.style.background = "#f8f8f8");

                    let selectedLabel = scaleDiv.querySelector(`label[for='${this.id}']`);
                    if (selectedLabel) {
                        selectedLabel.style.background = "#4CAF50";
                    }
                });
            });

            const submitBtn = document.getElementById("submitBtn");
            submitBtn.addEventListener("click", function() {
                submitBtn.classList.add("clicked");
                calculateResults();
            });

            function calculateResults() {
                let scores = {};
                let selected = document.querySelectorAll("input:checked");

                if (selected.length === 0) {
                    alert("Please select at least one answer before submitting.");
                    return;
                }

                selected.forEach(input => {
                    let gift = input.getAttribute("data-gift");
                    let value = parseInt(input.value);
                    if (gift) {
                        scores[gift] = (scores[gift] || 0) + value;
                    }
                });

                let sortedGifts = Object.entries(scores)
                    .sort((a, b) => b[1] - a[1])
                    .slice(0, 5);

                let resultsList = document.getElementById("resultsList");
                resultsList.innerHTML = "";

                sortedGifts.forEach(([gift, score]) => {
                    let li = document.createElement("li");
                    li.textContent = `${gift}: ${score} points`;
                    resultsList.appendChild(li);
                });

                document.getElementById("results").style.display = "block";
            }
        });
    </script>
</body>
</html>
