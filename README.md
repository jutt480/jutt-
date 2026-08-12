<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <meta name="theme-color" content="#059669" />
    <meta name="description" content="Ashif FeedPro - Feed Formulation & LP Least-Cost Optimizer Desktop Software" />
    <link rel="manifest" href="/manifest.json" />
    <title>Ashif FeedPro - Feed Formulation & LP Least-Cost Optimizer</title>
  </head>
  <body class="bg-slate-950 text-slate-100 antialiased selection:bg-emerald-500 selection:text-white">
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
    <script>
      if ('serviceWorker' in navigator) {
        window.addEventListener('load', () => {
          navigator.serviceWorker.register('/sw.js').catch(err => console.log('SW registration error:', err));
        });
      }
    </script>
  </body>
</html>
