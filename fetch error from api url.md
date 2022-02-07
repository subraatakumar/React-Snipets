
# fetch error from api url

~~~javascript
const [items, setItems] = useState([]);
const [fetchError, setFetchError] = useState(null);
const [isLoading, setIsLoading] = useState(true); // isLoading is true at beginning

useEffect(()=>{
  const fetchItems = async () => {
    try{
      const response = await fetch(API_URL);
      if(!response.ok) throw Error('Did not received expected data');
      const listItems = await response.json();
      setItems(listItems);
      setFetchError(null);
    } catch(err){
      console.log(err.message);
      setFetchError(err.message);
    } finally {
      setIsLoading(false);
    }
  }
  
  fetchItems();
},[]) // Loads once at program loading
~~~

## Display fetch error in the desired location

~~~javascript
{fetchError && <p style={{color: "red"}}>{`Error: ${fetchError}`}</p>}
~~~
