# Sistema de Análisis de Ventas ⚙️

A **.NET 8 Worker Service** scaffolded as the foundation for a background sales analysis system. This project demonstrates the **hosted service pattern** in .NET, where long-running background tasks are managed by the .NET generic host with built-in dependency injection, logging, and cancellation token support.

---

## 📋 Description

This project uses the **.NET Worker Service** template to create a hosted background process. The Worker class extends BackgroundService and runs continuously, logging execution timestamps at 1-second intervals. It serves as the backbone for a sales analysis system where background processing (ETL, report generation, data aggregation) would run independently of any web request cycle.

---

## ✨ Features

- ⚙️ **Hosted Background Service** — Runs as a long-lived process managed by .NET Generic Host
- 🔄 **Continuous Execution Loop** — ExecuteAsync with CancellationToken for graceful shutdown
- 📝 **Structured Logging** — ILogger<Worker> with LogLevel.Information
- 🛑 **Graceful Cancellation** — Respects CancellationToken for safe shutdown
- 💉 **Dependency Injection** — Services injected via constructor

---

## 🛠️ Technologies

| Category | Technology |
|----------|-----------|
| Language | C# |
| Framework | .NET 8 Worker Service |
| Pattern | Hosted Service (BackgroundService) |
| Logging | Microsoft.Extensions.Logging |
| Host | .NET Generic Host |

---

## 🏗️ Architecture

```
Sistema-de-analisis-de-ventas/
├── Program.cs       Generic Host setup — registers Worker, logging, DI container
├── Worker.cs        BackgroundService implementation
│                    └── ExecuteAsync(CancellationToken) — main loop
└── appsettings.json Logging configuration (LogLevel settings)
```

---

## 🔑 Core Pattern

```csharp
public class Worker : BackgroundService
{
    private readonly ILogger<Worker> _logger;

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            _logger.LogInformation("Worker running at: {time}", DateTimeOffset.Now);
            await Task.Delay(1000, stoppingToken);  // Non-blocking 1s interval
        }
    }
}
```

---

## 🚀 How to Run

Prerequisites: .NET 8 SDK

```bash
git clone https://github.com/Eithan22/Sistema-de-analisis-de-ventas.git
cd Sistema-de-analisis-de-ventas
dotnet run
```

The worker will start and log timestamps every second. Press Ctrl+C to trigger graceful shutdown via CancellationToken.

---

## 💡 Skills Demonstrated

- ✅ **Worker Service Pattern** — .NET BackgroundService for long-running processes
- ✅ **CancellationToken** — Proper async cancellation for graceful shutdown
- ✅ **Dependency Injection** — Logger injected via constructor
- ✅ **async/await** — Non-blocking execution with Task.Delay
- ✅ **.NET Generic Host** — Host builder with service registration

---

## 🔮 Future Improvements

- [ ] Integrate ETL pipeline (CSV reading + SQL Server loading)
- [ ] Add configurable scheduling (every X hours/minutes)
- [ ] Connect to sales database for real data aggregation
- [ ] Add health checks endpoint
- [ ] Deploy as Windows Service or Docker container

---

## 👨‍💻 Author

**Eithan** — Backend Developer · Santo Domingo, Dominican Republic 🇩🇴
🎓 Software Development @ ITLA · 📧 eithanread1@gmail.com
[LinkedIn](https://linkedin.com/in/eithan-r) · [GitHub](https://github.com/Eithan22)

---

*MIT License*
