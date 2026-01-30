# github.io-dashboard00 Dashboard de vendas
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Business Intelligence Dashboard</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        body { background-color: #0f172a; color: #f8fafc; font-family: 'Inter', sans-serif; }
        .card { background: #1e293b; border: 1px solid #334155; transition: transform 0.2s; }
        .card:hover { transform: translateY(-5px); border-color: #3b82f6; }
        .btn-primary { background: #3b82f6; transition: 0.3s; }
        .btn-primary:hover { background: #2563eb; box-shadow: 0 0 15px rgba(59, 130, 246, 0.5); }
    </style>
</head>
<body class="p-8">

    <div class="max-w-7xl mx-auto">
        <header class="flex flex-col md:flex-row justify-between items-center mb-10 gap-4">
            <div>
                <h1 class="text-3xl font-extrabold tracking-tight">Data<span class="text-blue-500">Analyzer</span> Pro</h1>
                <p class="text-slate-400 text-sm">Painel de controle de métricas e performance</p>
            </div>
            
            <div class="flex gap-3">
                <label class="btn-primary cursor-pointer text-white px-5 py-2.5 rounded-xl font-semibold flex items-center gap-2 shadow-lg">
                    <i class="fas fa-file-import"></i> Importar (Excel/SQL)
                    <input type="file" class="hidden" id="fileImport">
                </label>
                <button onclick="window.location.reload()" class="bg-slate-700 hover:bg-slate-600 text-white px-5 py-2.5 rounded-xl font-semibold flex items-center gap-2 transition">
                    <i class="fas fa-sync-alt"></i> Atualizar
                </button>
            </div>
        </header>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-10 text-center">
            <div class="card p-6 rounded-2xl">
                <p class="text-slate-400 text-xs font-bold uppercase mb-1">Faturamento Total</p>
                <h2 class="text-3xl font-bold">R$ 142.5K</h2>
                <p class="text-emerald-400 text-xs mt-2"><i class="fas fa-caret-up"></i> 8.2% vs mês anterior</p>
            </div>
            <div class="card p-6 rounded-2xl text-center">
                <p class="text-slate-400 text-xs font-bold uppercase mb-1">Margem Média</p>
                <h2 class="text-3xl font-bold">44.5%</h2>
                <p class="text-slate-500 text-xs mt-2">Dentro da meta global</p>
            </div>
            <div class="card p-6 rounded-2xl text-center">
                <p class="text-slate-400 text-xs font-bold uppercase mb-1">Volume Mensal</p>
                <h2 class="text-3xl font-bold">1,240</h2>
                <p class="text-red-400 text-xs mt-2"><i class="fas fa-caret-down"></i> 1.5% instável</p>
            </div>
            <div class="card p-6 rounded-2xl text-center">
                <p class="text-slate-400 text-xs font-bold uppercase mb-1">Satisfação</p>
                <h2 class="text-3xl font-bold">4.9/5</h2>
                <div class="flex justify-center text-yellow-400 text-[10px] mt-2">
                    <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
                </div>
            </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            
            <div class="card p-6 rounded-2xl lg:col-span-2">
                <h3 class="font-bold mb-6 flex items-center gap-2"><i class="fas fa-chart-line text-blue-500"></i> Evolução de Vendas</h3>
                <canvas id="lineChart" height="120"></canvas>
            </div>

            <div class="card p-6 rounded-2xl">
                <h3 class="font-bold mb-6 flex items-center gap-2"><i class="fas fa-chart-pie text-purple-500"></i> Distribuição por Marca</h3>
                <canvas id="donutChart"></canvas>
            </div>

            <div class="card p-6 rounded-2xl lg:col-span-1">
                <h3 class="font-bold mb-6 flex items-center gap-2"><i class="fas fa-chart-bar text-emerald-500"></i> Top Produtos</h3>
                <canvas id="barChart"></canvas>
            </div>

            <div class="card p-6 rounded-2xl lg:col-span-2">
                <h3 class="font-bold mb-6 flex items-center gap-2"><i class="fas fa-layer-group text-orange-500"></i> Performance por Região (Empilhado)</h3>
                <canvas id="stackedChart" height="120"></canvas>
            </div>

        </div>
    </div>

    <script>
        // Configurações Globais do Chart.js para Dark Mode
        Chart.defaults.color = '#94a3b8';
        Chart.defaults.borderColor = '#334155';

        // 1. Gráfico de Linha
        new Chart(document.getElementById('lineChart'), {
            type: 'line',
            data: {
                labels: ['Jan', 'Fev', 'Mar', 'Abr', 'Mai', 'Jun'],
                datasets: [{
                    label: 'Vendas 2024',
                    data: [65, 59, 80, 81, 56, 95],
                    borderColor: '#3b82f6',
                    backgroundColor: 'rgba(59, 130, 246, 0.1)',
                    fill: true,
                    tension: 0.4
                }]
            }
        });

        // 2. Gráfico de Rosca
        new Chart(document.getElementById('donutChart'), {
            type: 'doughnut',
            data: {
                labels: ['Marca ABC', 'Marca 123', 'Outras'],
                datasets: [{
                    data: [45, 30, 25],
                    backgroundColor: ['#3b82f6', '#a855f7', '#1e293b'],
                    borderWidth: 0
                }]
            },
            options: { cutout: '70%' }
        });

        // 3. Gráfico de Barras
        new Chart(document.getElementById('barChart'), {
            type: 'bar',
            data: {
                labels: ['Creatina', 'Whey', 'Ômega 3', 'BCAA'],
                datasets: [{
                    label: 'Qtd Vendida',
                    data: [300, 450, 200, 150],
                    backgroundColor: '#10b981',
                    borderRadius: 5
                }]
            }
        });

        // 4. Gráfico de Barras Empilhadas
        new Chart(document.getElementById('stackedChart'), {
            type: 'bar',
            data: {
                labels: ['SP', 'RJ', 'MG', 'ES', 'PR'],
                datasets: [
                    { label: 'Venda Direta', data: [12, 19, 3, 5, 2], backgroundColor: '#3b82f6' },
                    { label: 'Online', data: [8, 11, 5, 8, 3], backgroundColor: '#f97316' }
                ]
            },
            options: {
                scales: { x: { stacked: true }, y: { stacked: true } }
            }
        });
    </script>
</body>
</html>
