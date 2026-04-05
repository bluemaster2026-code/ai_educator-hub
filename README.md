<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI for Educators: Interactive Learning Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #f5f5f4; 
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #d6d3d1; 
            border-radius: 4px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
            background: #a8a29e; 
        }
    </style>
</head>
<body class="bg-stone-50 text-stone-800 font-sans antialiased min-h-screen flex flex-col">

    <!-- Chosen Palette: Warm Neutrals with Teal and Amber Accents -->
    <!-- Application Structure Plan: The SPA is structured as a two-part learning dashboard. The top section introduces the impact of AI in education using a comparative chart to establish value and motivation. The bottom section is an interactive video catalog (left column) paired with a dynamic learning pane (right column). This layout was chosen because it allows students to browse topics without losing context of their current lesson and immediately presents the practical activity alongside the theoretical video content, reinforcing active learning. -->
    <!-- Visualization & Content Choices: 1. Impact Chart -> Goal: Inform/Compare -> Bar Chart (Chart.js) -> Shows time saved across educational tasks to motivate learning -> Justification: Clearly visualizes the 'why' before the 'how'. 2. Interactive Video Catalog -> Goal: Organize/Explore -> Filterable List + Detail View -> Users select categories to find relevant modules -> Justification: Keeps the interface clean while offering depth. 3. Practical Activities -> Goal: Inform/Apply -> Contextual Text Block -> Updates based on video selection -> Justification: Direct application of knowledge. NO SVG/Mermaid used. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <header class="bg-white shadow-sm border-b border-stone-200 py-6 px-4 md:px-8 sticky top-0 z-10">
        <div class="max-w-7xl mx-auto flex justify-between items-center">
            <div>
                <h1 class="text-2xl md:text-3xl font-bold text-stone-900 tracking-tight">AI for Educators <span class="text-teal-600">Learning Hub</span></h1>
                <p class="text-sm text-stone-500 mt-1">Master artificial intelligence tools to enhance teaching, grading, and administration.</p>
            </div>
            <div class="hidden md:flex space-x-4 text-2xl">
                <span>🎓</span>
                <span>🤖</span>
                <span>📚</span>
            </div>
        </div>
    </header>

    <main class="flex-grow max-w-7xl mx-auto w-full p-4 md:p-8 flex flex-col gap-8">

        <section class="bg-white rounded-xl shadow-sm border border-stone-100 p-6 md:p-8">
            <div class="max-w-3xl mx-auto text-center mb-8">
                <h2 class="text-xl md:text-2xl font-semibold text-stone-800 mb-4">Why Integrate AI into Your Workflow?</h2>
                <p class="text-stone-600 leading-relaxed">
                    This section provides a data-driven look at how AI tools can transform your weekly schedule. The chart below illustrates the average hours educators spend on administrative and planning tasks conventionally, compared to the projected time spent when effectively utilizing AI assistants. Understanding this impact is your first step before diving into the video modules.
                </p>
            </div>
            
            <div class="w-full flex justify-center">
                <div class="chart-container">
                    <canvas id="impactChart"></canvas>
                </div>
            </div>
        </section>

        <section class="flex flex-col lg:flex-row gap-6 h-full">
            
            <div class="w-full lg:w-1/3 bg-white rounded-xl shadow-sm border border-stone-100 flex flex-col h-[600px]">
                <div class="p-4 border-b border-stone-100">
                    <h2 class="text-lg font-semibold text-stone-800 mb-3">Video Modules</h2>
                    <p class="text-xs text-stone-500 mb-4">Select a category and choose a video to start your lesson and practical activity.</p>
                    
                    <div class="flex flex-wrap gap-2" id="filter-container">
                    </div>
                </div>
                
                <div class="flex-grow overflow-y-auto custom-scrollbar p-2" id="video-list">
                </div>
            </div>

            <div class="w-full lg:w-2/3 bg-white rounded-xl shadow-sm border border-stone-100 flex flex-col min-h-[600px]" id="active-lesson-container">
                <div class="flex-grow flex items-center justify-center text-stone-400 flex-col p-8 text-center h-full">
                    <span class="text-5xl mb-4">🎬</span>
                    <h3 class="text-xl font-medium text-stone-700">Select a video module to begin</h3>
                    <p class="text-sm mt-2">Choose a topic from the menu on the left to load the video details and your practical assignment.</p>
                </div>
            </div>

        </section>

    </main>

    <footer class="bg-stone-900 text-stone-400 py-6 text-center text-sm">
        <p>Interactive SPA Dashboard &copy; 2026 Educator AI Initiative.</p>
    </footer>

    <script>
        const learningModules = [
            {
                id: 1,
                title: "Prompt Engineering Basics for Teachers",
                category: "Foundations",
                duration: "14 mins",
                icon: "🧠",
                description: "Learn the core principles of communicating effectively with Large Language Models (LLMs). We cover setting personas, providing context, defining constraints, and formatting outputs to get exactly what you need for your classroom.",
                activityTitle: "Draft Your First Teaching Persona Prompt",
                activitySteps: [
                    "Open your preferred AI tool (e.g., ChatGPT, Claude).",
                    "Write a prompt instructing the AI to act as an expert middle-school science teacher.",
                    "Ask it to explain a complex topic (like photosynthesis) to a 10-year-old.",
                    "Refine the prompt by asking it to use an analogy related to a factory."
                ],
                outcomes: "You will understand how context and constraints drastically improve AI outputs."
            },
            {
                id: 2,
                title: "Automating Weekly Lesson Plans",
                category: "Planning",
                duration: "22 mins",
                icon: "📅",
                description: "Discover how to transform state standards and curriculum goals into structured, day-by-day lesson plans in minutes. This module explores generating differentiation strategies and engaging hook activities.",
                activityTitle: "Generate a 3-Day Unit Plan",
                activitySteps: [
                    "Select a specific learning standard for your grade level.",
                    "Prompt the AI to create a 3-day sequential lesson plan based on that standard.",
                    "Request that Day 1 includes a collaborative activity, Day 2 includes direct instruction, and Day 3 is a formative assessment.",
                    "Review and manually edit the AI's output to fit your specific classroom context."
                ],
                outcomes: "You will have a working template for rapidly generating aligned, structured lesson plans."
            },
            {
                id: 3,
                title: "Creating Rubrics and Grading Assistants",
                category: "Grading",
                duration: "18 mins",
                icon: "✅",
                description: "Learn to use AI to generate highly specific grading rubrics and how to use it to provide baseline constructive feedback on student writing, saving hours of weekend grading.",
                activityTitle: "Build a Custom Rubric",
                activitySteps: [
                    "Identify an upcoming assignment (e.g., a persuasive essay).",
                    "Ask the AI to generate a 4-point scale rubric for this assignment.",
                    "Ensure you specify the criteria: Thesis Clarity, Evidence, Grammar, and Formatting.",
                    "Provide a short, dummy student paragraph to the AI and ask it to evaluate it based on the newly created rubric."
                ],
                outcomes: "You will automate the creation of assessment tools and streamline the feedback process."
            },
            {
                id: 4,
                title: "Interactive Quiz Generation",
                category: "Engagement",
                duration: "15 mins",
                icon: "❓",
                description: "Quickly turn reading materials, textbook chapters, or your own notes into multiple-choice, true/false, or short-answer quizzes suitable for platforms like Kahoot or Google Forms.",
                activityTitle: "Text-to-Quiz Transformation",
                activitySteps: [
                    "Find a short article or text excerpt relevant to your subject.",
                    "Paste the text into the AI and prompt it to generate 5 multiple-choice questions.",
                    "Specify that each question must have 4 options and clearly indicate the correct answer.",
                    "Ask the AI to format the output as a CSV table so it can be easily imported into quiz software."
                ],
                outcomes: "You will learn to rapidly deploy formative assessments without manual question writing."
            },
            {
                id: 5,
                title: "Drafting Parent Communications",
                category: "Admin",
                duration: "10 mins",
                icon: "✉️",
                description: "Tackle the administrative burden of parent emails, weekly newsletters, and behavioral reports. Learn how to maintain a professional, empathetic tone using AI drafting.",
                activityTitle: "Draft a Positive Intervention Email",
                activitySteps: [
                    "Think of a scenario where a student has recently improved their behavior or academic performance.",
                    "Prompt the AI to draft an email to the parents celebrating this success.",
                    "Instruct the AI to keep the tone warm, professional, and concise (under 150 words).",
                    "Practice adjusting the tone by asking the AI to make it slightly more formal."
                ],
                outcomes: "You will reduce anxiety and time spent on routine administrative communications."
            },
            {
                id: 6,
                title: "Differentiating Content for IEPs",
                category: "Planning",
                duration: "25 mins",
                icon: "🧩",
                description: "Utilize AI to instantly adjust reading levels, translate materials, or reformat instructions to meet the specific accommodations outlined in student Individualized Education Programs (IEPs).",
                activityTitle: "Reading Level Adjustment",
                activitySteps: [
                    "Take a standard grade-level reading passage.",
                    "Prompt the AI to rewrite the exact same narrative but lower the reading level by two grades.",
                    "Ask the AI to highlight or bold key vocabulary words in the new text.",
                    "Ask the AI to generate three basic comprehension questions specifically for the simplified text."
                ],
                outcomes: "You will confidently adapt core materials for diverse learning needs on the fly."
            }
        ];

        let currentCategory = 'All';

        function initApp() {
            renderFilters();
            renderVideoList();
            initChart();
        }

        function renderFilters() {
            const categories = ['All', ...new Set(learningModules.map(m => m.category))];
            const filterContainer = document.getElementById('filter-container');
            filterContainer.innerHTML = '';

            categories.forEach(category => {
                const btn = document.createElement('button');
                btn.className = `px-3 py-1.5 text-xs font-medium rounded-full transition-colors duration-200 border ${currentCategory === category ? 'bg-stone-800 text-white border-stone-800' : 'bg-white text-stone-600 border-stone-200 hover:bg-stone-100'}`;
                btn.textContent = category;
                btn.onclick = () => {
                    currentCategory = category;
                    renderFilters();
                    renderVideoList();
                };
                filterContainer.appendChild(btn);
            });
        }

        function renderVideoList() {
            const listContainer = document.getElementById('video-list');
            listContainer.innerHTML = '';

            const filteredModules = currentCategory === 'All' 
                ? learningModules 
                : learningModules.filter(m => m.category === currentCategory);

            filteredModules.forEach(module => {
                const card = document.createElement('div');
                card.className = 'p-3 mb-2 rounded-lg border border-stone-100 bg-stone-50 hover:bg-white hover:shadow-sm hover:border-teal-100 cursor-pointer transition-all duration-200 flex items-start gap-3';
                card.onclick = () => renderActiveLesson(module);
                
                card.innerHTML = `
                    <div class="text-2xl mt-1">${module.icon}</div>
                    <div>
                        <h4 class="text-sm font-semibold text-stone-800 leading-tight">${module.title}</h4>
                        <div class="flex items-center gap-2 mt-1">
                            <span class="text-[10px] uppercase tracking-wider font-bold text-teal-600 bg-teal-50 px-1.5 py-0.5 rounded">${module.category}</span>
                            <span class="text-xs text-stone-500">⏱ ${module.duration}</span>
                        </div>
                    </div>
                `;
                listContainer.appendChild(card);
            });
        }

        function renderActiveLesson(module) {
            const container = document.getElementById('active-lesson-container');
            
            let stepsHtml = '';
            module.activitySteps.forEach((step, index) => {
                stepsHtml += `<li class="flex gap-3 text-stone-700 text-sm mb-3">
                    <span class="flex-shrink-0 w-6 h-6 rounded-full bg-amber-100 text-amber-700 flex items-center justify-center font-bold text-xs">${index + 1}</span>
                    <span class="mt-0.5">${step}</span>
                </li>`;
            });

            container.innerHTML = `
                <div class="p-6 md:p-8 flex flex-col h-full overflow-y-auto custom-scrollbar">
                    <div class="flex items-center gap-2 mb-4">
                        <span class="text-xs font-bold uppercase tracking-wider text-teal-600 bg-teal-50 px-2 py-1 rounded-md">${module.category}</span>
                        <span class="text-xs text-stone-500 font-medium">${module.duration} Module</span>
                    </div>
                    
                    <h2 class="text-2xl md:text-3xl font-bold text-stone-900 mb-4">${module.icon} ${module.title}</h2>
                    
                    <div class="bg-stone-900 w-full rounded-xl aspect-video mb-6 flex items-center justify-center relative overflow-hidden shadow-md">
                        <div class="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent"></div>
                        <button class="w-16 h-16 bg-white/20 hover:bg-teal-500 backdrop-blur-sm rounded-full flex items-center justify-center transition-colors duration-300 z-10 group">
                            <span class="text-white text-2xl ml-1 group-hover:scale-110 transition-transform">▶</span>
                        </button>
                        <span class="absolute bottom-4 left-4 text-white text-sm font-medium z-10">Simulated Video Player</span>
                    </div>

                    <div class="mb-8">
                        <h3 class="text-lg font-semibold text-stone-800 mb-2 border-b border-stone-100 pb-2">Module Overview</h3>
                        <p class="text-stone-600 text-sm leading-relaxed">${module.description}</p>
                    </div>

                    <div class="bg-amber-50 rounded-xl p-6 border border-amber-100 mt-auto shadow-inner">
                        <div class="flex items-center gap-2 mb-4">
                            <span class="text-xl">✍️</span>
                            <h3 class="text-lg font-bold text-amber-900">Practical Activity: ${module.activityTitle}</h3>
                        </div>
                        <ul class="mb-4">
                            ${stepsHtml}
                        </ul>
                        <div class="bg-white p-4 rounded-lg border border-amber-200 mt-4">
                            <p class="text-sm font-medium text-amber-800"><span class="font-bold">🎯 Expected Outcome:</span> ${module.outcomes}</p>
                        </div>
                    </div>
                </div>
            `;
        }

        function initChart() {
            const ctx = document.getElementById('impactChart').getContext('2d');
            
            new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Lesson Planning', 'Grading & Feedback', 'Admin/Emails', 'Resource Creation'],
                    datasets: [
                        {
                            label: 'Traditional Hours/Week',
                            data: [8, 10, 5, 4],
                            backgroundColor: '#d6d3d1',
                            borderRadius: 4
                        },
                        {
                            label: 'Hours/Week with AI',
                            data: [2, 4, 1.5, 1],
                            backgroundColor: '#0d9488', 
                            borderRadius: 4
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'top',
                            labels: {
                                font: {
                                    family: "'Inter', sans-serif",
                                    size: 12
                                },
                                usePointStyle: true,
                                boxWidth: 8
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(28, 25, 23, 0.9)',
                            titleFont: { size: 13, family: "'Inter', sans-serif" },
                            bodyFont: { size: 13, family: "'Inter', sans-serif" },
                            padding: 10,
                            callbacks: {
                                label: function(context) {
                                    return context.dataset.label + ': ' + context.parsed.y + ' hrs';
                                }
                            }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            title: {
                                display: true,
                                text: 'Hours per Week',
                                font: {
                                    family: "'Inter', sans-serif",
                                    size: 12
                                }
                            },
                            grid: {
                                color: '#f5f5f4'
                            }
                        },
                        x: {
                            grid: {
                                display: false
                            },
                            ticks: {
                                font: {
                                    family: "'Inter', sans-serif",
                                    size: 11
                                },
                                callback: function(value) {
                                    let label = this.getLabelForValue(value);
                                    if (label.length > 16) {
                                        let splitPos = label.indexOf(' ', 10);
                                        if (splitPos !== -1) {
                                            return [label.substring(0, splitPos), label.substring(splitPos + 1)];
                                        }
                                    }
                                    return label;
                                }
                            }
                        }
                    }
                }
            });
        }

        window.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html># ai_educator-hub
AI Educator resources
