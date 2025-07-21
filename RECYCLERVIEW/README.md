# RECYCLERVIEW

## Step 1 - Create a ViewHolder

```bash
class InfoSabadosViewHolder(itemView: View): ViewHolder(itemView){
    val titleView = itemView.findViewById<TextView>(R.id.dateTitle)
    val descriptionView = itemView.findViewById<TextView>(R.id.dateTitle)
}
```

## Step 2 - Create an Adapter

```bash
class InfoSabadosAdapter(): RecyclerView.Adapter<InfoSabadosViewHolder>() {

    var itemList = emptyList<InfoSabados>()

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): InfoSabadosViewHolder {
        val view = LayoutInflater.from(parent.context).inflate(R.layout.recycler_item_sabados, parent, false)
        return InfoSabadosViewHolder(view)
    }

    override fun getItemCount(): Int {
        return itemList.size
    }

    override fun onBindViewHolder(holder: InfoSabadosViewHolder, position: Int) {
        val item = itemList[position]
        holder.titleView.text = item.data
        holder.descriptionView.text = item.description

    }

    //Notify Data is ready
    fun setItems(items: List<InfoSabados>) {
        itemList = items
        notifyDataSetChanged()
    }
}
```

## Step 3 - Get LiveData on the ViewModel

```bash
class SabadosViewModel: ViewModel() {

    private var _items: MutableLiveData<List<InfoSabados>> = MutableLiveData()
    val items: LiveData<List<InfoSabados>> = _items


    private fun loadItems() {
        val temp = ArrayList<InfoSabados>()
        temp.add(InfoSabados("Test1", "Test1"))
        temp.add(InfoSabados("Test2", "Test2"))
        temp.add(InfoSabados("Test3", "Test3"))
        temp.add(InfoSabados("Test4", "Test4"))
        _items.value = temp
    }
}
```

## Step 4 - Set Up everythin on the Activity/Fragment

```bash
class SabadosFragment : BaseNavigationFragment(R.layout.fragment_courier_sabado) {

    private lateinit var viewModel: SabadosViewModel
    private lateinit var adapter: InfoSabadosAdapter

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        val recyclerView = view.findViewById<RecyclerView>(R.id.recyclerView_expPlataforma_sabado)
        recyclerView.layoutManager = LinearLayoutManager(context)
        adapter = InfoSabadosAdapter()
        recyclerView.adapter = adapter
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        //Use ViewModelProvider to survive configuration changes
        //If you do this:  viewModel = ViewModel() it will create one each time
        viewModel = ViewModelProvider(this)[SabadosViewModel::class.java]
        
        viewModel.items.observe(this) { items ->
            adapter.setItems(items)
        }
        
        viewModel.loadItems()
    }
}
```
