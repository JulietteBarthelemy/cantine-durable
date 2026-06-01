# cantine-d<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Suivi des Déchets - Notre Collège s'engage</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            background-color: #f7faf7; 
            color: #2d3748; 
            margin: 0; 
            padding: 20px; 
        }
        .wrapper { 
            max-width: 900px; 
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
        
        .bloc-dechets { 
            display: grid; 
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); 
            gap: 20px; 
            margin-bottom: 35px;
        }
        .carte { 
            background: white; 
            padding: 20px; 
            border-radius: 12px; 
            text-align: center; 
            box-shadow: 0 4px 6px rgba(0,0,0,0.05); 
            border-top: 6px solid #4cbd7a; 
        }
        .carte h3 { margin: 0 0 10px 0; color: #1b4d3e; font-size: 18px; }
        .carte p { font-size: 14px; color: #718096; margin: 0 0 15px 0; }
        .poids-affiche { font-size: 32px; font-weight: bold; color: #dd6b20; }

        /* --- STYLE DU TABLEAU --- */
        .zone-tableau {
            background: white;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }
        .zone-tableau h2 {
            color: #1b4d3e;
            margin-top: 0;
            margin-bottom: 20px;
        }
        table {
            width: 100%;
            border-collapse: collapse; /* Aligne les bordures */
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
            background-color: #f1f7f4; /* Effet de survol de la ligne */
        }
        .total-ligne {
            font-weight: bold;
            background-color: #edf2f7;
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
            <p>Pour agir concrètement en faveur d'une consommation responsable, nos éco-délégués mesurent chaque jour la quantité de déchets générés à la cantine. Voici le bilan actuel de nos 5 zones de tri :</p>
        </section>

        <!-- Les cartes (poubelles visuelles) -->
        <main class="bloc-dechets">
            <div class="carte">
                <h3>Déchets Alimentaires</h3>
                <p>Restes des plats et des assiettes</p>
                <div class="poids-affiche">15.2 kg</div>
            </div>

            <div class="carte">
                <h3>Le Pain</h3>
                <p>Morceaux de pain gaspillés</p>
                <div class="poids-affiche">4.1 kg</div>
            </div>

            <div class="carte">
                <h3>Fruits entamés</h3>
                <p>Fruits non finis</p>
                <div class="poids-affiche">2.3 kg</div>
            </div>

            <div class="carte">
                <h3>Serviettes en papier</h3>
                <p>Serviettes à jeter</p>
                <div class="poids-affiche">0.9 kg</div>
            </div>

            <div class="carte">
                <h3>Emballages</h3>
                <p>Pots de yaourt, plastiques...</p>
                <div class="poids-affiche">3.5 kg</div>
            </div>
        </main>

        <!-- LE TABLEAU RECAPITULATIF -->
        <section class="zone-tableau">
            <h2>Tableau de synthèse des pesées</h2>
            <table>
                <thead>
                    <tr>
                        <th>Type de Déchet / Poubelle</th>
                        <th>Poids Mesuré (kg)</th>
                        <th>Objectif de Réduction</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td><strong>Déchets Alimentaires</strong></td>
                        <td>15.2 kg</td>
                        <td>Passer sous la barre des 10 kg</td>
                    </tr>
                    <tr>
                        <td><strong>Le Pain</strong></td>
                        <td>4.1 kg</td>
                        <td>Objectif : Zéro gâchis de pain</td>
                    </tr>
                    <tr>
                        <td><strong>Fruits entamés</strong></td>
                        <td>2.3 kg</td>
                        <td>Sensibiliser au gaspillage des fruits</td>
                    </tr>
                    <tr>
                        <td><strong>Serviettes en papier</strong></td>
                        <td>0.9 kg</td>
                        <td>Prendre 1 seule serviette max</td>
                    </tr>
                    <tr>
                        <td><strong>Emballages</strong></td>
                        <td>3.5 kg</td>
                        <td>Favoriser le vrac en cuisine</td>
                    </tr>
                    <!-- Ligne du total -->
                    <tr class="total-ligne">
                        <td>TOTAL DES DÉCHETS (sur 1 repas)</td>
                        <td>26.0 kg</td>
                        <td>Pour 700 demi-pensionnaires</td>
                    </tr>
                </tbody>
            </table>
        </section>

        <footer>
            <p>© 2026 Projet Éco-Collège Vaucluse - Sensibilisation à l'ODD 12</p>
        </footer>

    </div>

</body>
</html>urable
