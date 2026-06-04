<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Suivi des Déchets - Notre Collège s'engage</title>
    <!-- Intégration de Chart.js pour un graphique dynamique -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            background-color: #f7faf7; 
            color: #2d3748; 
            margin: 0; 
            padding: 20px; 
        }
        .wrapper { 
            max-width: 1000px; 
            margin: 0 auto; 
        }
        header { 
            background-color: #1b4d3e; 
            color: white; 
            padding: 30px; 
            text-align: center; 
            border-radius: 12px;
            margin-bottom: 25px;
        }
        header h1 { margin: 0 0 10px 0; font-size: 24px; }
        header p { margin: 0; font-size: 16px; opacity: 0.9; }
        
        .presentation { 
            background: white; 
            padding: 20px; 
            border-radius: 12px; 
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            margin-bottom: 25px;
        }

        /* --- FORMULAIRE DE SAISIE --- */
        .zone-saisie {
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            margin-bottom: 25px;
            border-left: 6px solid #1b4d3e;
        }
        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }
        .form-group {
            display: flex;
            flex-direction: column;
        }
        .form-group label {
            font-size: 12px;
            font-weight: bold;
            margin-bottom: 5px;
            color: #4a5568;
        }
        .form-group input {
            padding: 8px;
            border: 1px solid #cbd5e0;
            border-radius: 6px;
            font-size: 14px;
        }
        .btn-ajouter {
            background-color: #1b4d3e;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: bold;
            align-self: flex-end;
            transition: background 0.2s;
        }
        .btn-ajouter:hover {
            background-color: #2c6b56;
        }
        
        .bloc-dechets { 
            display: grid; 
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); 
            gap: 15px; 
            margin-bottom: 35px;
        }
        .carte { 
            background: white; 
            padding: 15px; 
            border-radius: 12px; 
            text-align: center; 
            box-shadow: 0 4px 6px rgba(0,0,0,0.05); 
            border-top: 6px solid #4cbd7a; 
        }
        .carte h3 { margin: 0 0 5px 0; color: #1b4d3e; font-size: 16px; }
        .carte p { font-size: 12px; color: #718096; margin: 0 0 10px 0; }
        .poids-affiche { font-size: 26px; font-weight: bold; color: #dd6b20; }

        .dashboard-visuel {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
            margin-bottom: 35px;
        }
        @media (max-width: 768px) {
            .dashboard-visuel { grid-template-columns: 1fr; }
        }

        /* --- STYLE DU TABLEAU --- */
        .zone-tableau, .zone-graphique {
            background: white;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }
        .zone-tableau h2, .zone-graphique h2 {
            color: #1b4d3e;
            margin-top: 0;
            margin-bottom: 20px;
        }
        table {
            width: 100%;
            border-collapse: collapse; 
            margin-top: 10px;
        }
        th, td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid #e2e8f0;
        }
        th {
            background-color: #1b4d3e;
            color: white;
            font-weight: bold;
        }
        tr:hover {
            background-color: #f1f7f4; 
        }
        .total-ligne {
            font-weight: bold;
            background-color: #edf2f7;
        }
        .ratio-eleve {
            font-size: 14px;
            color: #4a5568;
            margin-top: 5px;
            font-style: italic;
        }

        footer { 
            text-align: center; 
            margin-top: 50px; 
            font-size: 14px; 
            color: #a0aec0; 
        }
    </style>
</head>
<body>

    <div class="wrapper">

        <header>
            <h1>Objectifs de Développement Durable (ODD)</h1>
            <p>Collège du Vaucluse — Suivi du gaspillage de la cantine (700 demi-pensionnaires)</p>
        </header>

        <section class="presentation">
            <h2>Notre démarche anti-gâchis (ODD 12)</h2>
            <p>Pour agir concrètement en faveur d'une consommation responsable, nos éco-délégués mesurent chaque jour la quantité de déchets générés à la cantine. Utilisez le simulateur ci-dessous pour mettre à jour les données en temps réel.</p>
        </section>

        <!-- FORMULAIRE DE SAISIE EN DIRECT -->
        <section class="zone-saisie">
            <h3>Mettre à jour les pesées du repas</h3>
            <div class="form-grid">
                <div class="form-group">
                    <label for="input-alim">Alimentaire (kg)</label>
                    <input type="number" id="input-alim" value="15.2" step="0.1" min="0">
                </div>
                <div class="form-group">
                    <label for="input-pain">Le Pain (kg)</label>
                    <input type="number" id="input-pain" value="4.1" step="0.1" min="0">
                </div>
                <div class="form-group">
                    <label for="input-fruits">Fruits (kg)</label>
                    <input type="number" id="input-fruits" value="2.3" step="0.1" min="0">
                </div>
                <div class="form-group">
                    <label for="input-serviettes">Serviettes (kg)</label>
                    <input type="number" id="input-serviettes" value="0.9" step="0.1" min="0">
                </div>
                <div class="form-group">
                    <label for="input-emballages">Emballages (kg)</label>
                    <input type="number" id="input-emballages" value="3.5" step="0.1" min="0">
                </div>
                <button class="btn-ajouter" onclick="mettreAJourDonnees()">Calculer</button>
            </div>
        </section>

        <!-- Les cartes (poubelles visuelles) -->
        <main class="bloc-dechets">
            <div class="carte">
                <h3>Déchets Alimentaires</h3>
                <p>Restes des assiettes</p>
                <div class="poids-affiche" id="card-alim">15.2 kg</div>
            </div>

            <div class="carte">
                <h3>Le Pain</h3>
                <p>Morceaux gaspillés</p>
                <div class="poids-affiche" id="card-pain">4.1 kg</div>
            </div>

            <div class="carte">
                <h3>Fruits entamés</h3>
                <p>Fruits non finis</p>
                <div class="poids-affiche" id="card-fruits">2.3 kg</div>
            </div>

            <div class="carte">
                <h3>Serviettes papier</h3>
                <p>Serviettes à jeter</p>
                <div class="poids-affiche" id="card-serviettes">0.9 kg</div>
            </div>

            <div class="carte">
                <h3>Emballages</h3>
                <p>Pots de yaourt...</p>
                <div class="poids-affiche" id="card-emballages">3.5 kg</div>
            </div>
        </main>

        <div class="dashboard-visuel">
            <!-- LE TABLEAU RECAPITULATIF -->
            <section class="zone-tableau">
                <h2>Tableau de synthèse</h2>
                <table>
                    <thead>
                        <tr>
                            <th>Type de Déchet</th>
                            <th>Poids (kg)</th>
                            <th>Objectif</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><strong>Déchets Alimentaires</strong></td>
                            <td id="tab-alim">15.2 kg</td>
                            <td>Passer sous les 10 kg</td>
                        </tr>
                        <tr>
                            <td><strong>Le Pain</strong></td>
                            <td id="tab-pain">4.1 kg</td>
                            <td>Objectif : Zéro gâchis</td>
                        </tr>
                        <tr>
                            <td><strong>Fruits entamés</strong></td>
                            <td id="tab-fruits">2.3 kg</td>
                            <td>Sensibiliser les élèves</td>
                        </tr>
                        <tr>
                            <td><strong>Serviettes en papier</strong></td>
                            <td id="tab-serviettes">0.9 kg</td>
                            <td>Prendre 1 seule serviette</td>
                        </tr>
                        <tr>
                            <td><strong>Emballages</strong></td>
                            <td id="tab-emballages">3.5 kg</td>
                            <td>Favoriser le vrac</td>
                        </tr>
                        <tr class="total-ligne">
                            <td>TOTAL (sur 1 repas)</td>
                            <td id="tab-total">26.0 kg</td>
                            <td>
                                <div>Pour 700 élèves</div>
                                <div class="ratio-eleve" id="ratio-eleve">Soit 37g par élève</div>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </section>

            <!-- LE GRAPHIQUE INTERACTIF -->
            <section class="zone-graphique">
                <h2>Répartition du gaspillage</h2>
                <canvas id="graphiqueDechets" width="100" height="100"></canvas>
            </section>
        </div>

        <footer>
            <p>© 2026 Projet Éco-Collège Vaucluse - Sensibilisation à l'ODD 12</p>
        </footer>

    </div>

    <!-- LOGIQUE DE L'APPLICATION -->
    <script>
        let monGraphique;

        // Fonction d'initialisation du graphique Chart.js
        function initialiserGraphique(alim, pain, fruits, serv, emb) {
            const ctx = document.getElementById('graphiqueDechets').getContext('2d');
            monGraphique = new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['Alimentaire', 'Pain', 'Fruits', 'Serviettes', 'Emballages'],
                    datasets: [{
                        data: [alim, pain, fruits, serv, emb],
                        backgroundColor: ['#dd6b20', '#4cbd7a', '#3182ce', '#e2e8f0', '#ecc94b'],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: { position: 'bottom' }
                    }
                }
            });
        }

        // Fonction principale pour mettre à jour l'application en direct
        function mettreAJourDonnees() {
            // 1. Récupération des valeurs du formulaire
            const alim = parseFloat(document.getElementById('input-alim').value) || 0;
            const pain = parseFloat(document.getElementById('input-pain').value) || 0;
            const fruits = parseFloat(document.getElementById('input-fruits').value) || 0;
            const serviettes = parseFloat(document.getElementById('input-serviettes').value) || 0;
            const emballages = parseFloat(document.getElementById('input-emballages').value) || 0;

            // 2. Calcul du total et du ratio par demi-pensionnaire (700 élèves)
            const total = alim + pain + fruits + serviettes + emballages;
            const gParEleve = Math.round((total / 700) * 1000);

            // 3. Mise à jour des cartes visuelles
            document.getElementById('card-alim').innerText = alim.toFixed(1) + " kg";
            document.getElementById('card-pain').innerText = pain.toFixed(1) + " kg";
            document.getElementById('card-fruits').innerText = fruits.toFixed(1) + " kg";
            document.getElementById('card-serviettes').innerText = serviettes.toFixed(1) + " kg";
            document.getElementById('card-emballages').innerText = emballages.toFixed(1) + " kg";

            // 4. Mise à jour du tableau
            document.getElementById('tab-alim').innerText = alim.toFixed(1) + " kg";
            document.getElementById('tab-pain').innerText = pain.toFixed(1) + " kg";
            document.getElementById('tab-fruits').innerText = fruits.toFixed(1) + " kg";
            document.getElementById('tab-serviettes').innerText = serviettes.toFixed(1) + " kg";
            document.getElementById('tab-emballages').innerText = emballages.toFixed(1) + " kg";
            document.getElementById('tab-total').innerText = total.toFixed(1) + " kg";
            document.getElementById('ratio-eleve').innerText = "Soit " + gParEleve + "g par élève";

            // 5. Mise à jour du graphique
            if (monGraphique) {
                monGraphique.data.datasets[0].data = [alim, pain, fruits, serviettes, emballages];
                monGraphique.update();
            }
        }

        // Charger le graphique au démarrage avec les données de base
        window.onload = function() {
            initialiserGraphique(15.2, 4.1, 2.3, 0.9, 3.5);
        };
    </script>
</body>
</html>
