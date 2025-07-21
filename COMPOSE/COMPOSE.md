# COMPOSE

## Dependencies

```bash
// ViewModel
    implementation("androidx.lifecycle:lifecycle-viewmodel-compose:2.6.2")
```

## Set up

Main Activity

```bash
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            StockTrackerTheme {
                Surface (
                    modifier = Modifier.fillMaxSize()
                ) {
                    StockTrackerApp()
                }
            }
        }
    }
}
```

StockTrackerApp

```bash
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun StockTrackerApp() {
    val scrollBehavior = TopAppBarDefaults.enterAlwaysScrollBehavior()
    Scaffold(
        modifier = Modifier.nestedScroll(scrollBehavior.nestedScrollConnection),
        topBar = { StockTopAppBar(scrollBehavior = scrollBehavior) }
    ) {
        Surface(
            modifier = Modifier.fillMaxSize().padding(it)
        ) {
            val viewModel: StockMainViewModel = viewModel()
            StockMain(
                stockUiState = viewModel.stockUiState,
                contentPadding = it,
            )
        }
    }
}

@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun StockTopAppBar(scrollBehavior: TopAppBarScrollBehavior, modifier: Modifier = Modifier) {
    CenterAlignedTopAppBar(
        scrollBehavior = scrollBehavior,
        title = {
            Text(
                text = "STOCK TRACKER APP",
                style = MaterialTheme.typography.headlineSmall,
            )
        },
        modifier = modifier
    )
}
```

StockMain

```bash
@Composable
fun StockMain(
    stockUiState: StockUiState,
    modifier: Modifier = Modifier,
    contentPadding: PaddingValues = PaddingValues(0.dp)
    ) {
    when (stockUiState) {
        is StockUiState.Loading -> LoadingScreen()
        is StockUiState.Success -> ResultScreen(stockUiState.stocks)
        is StockUiState.Error -> ErrorScreen()
    }
}

@Composable
fun ResultScreen(
    stocks: Stocks,
    modifier: Modifier = Modifier
) {
    Text(
        text = stocks.bars.get("NVDA").toString()
    )
}

@Composable
fun LoadingScreen(
    modifier: Modifier = Modifier
) {
    Text(
        text = "Loading"
    )
}

@Composable
fun ErrorScreen(
    modifier: Modifier = Modifier
) {
    Text(
        text = "Error"
    )
}
```
