# // component
useEffect(() => {
    const fetchDataFromApi = async () => {
      try {
        setIsLoading(true);

        const trainList = await RequestMap(TRAIN_LIST);
        console.log('Train List:', trainList);

        setData(trainList);
        setFullData(trainList);
      } catch (error) {
        console.error('Error fetching data:', error);
        setError(error.toString());
      } finally {
        setIsLoading(false);
        setActiveIndicator(false);
        setErrorIndicator(false);
        setTrainDate(TrainDate);

        setSelectedTrain('');

        setOpen(false);
        settOpen(false);
      }
    };
    fetchDataFromApi();
  }, [TRAIN_LIST, TrainDate]);

  # api using axios
//  
import axios from 'axios';<br>

export const RequestMap = async (url) => {<br>
  try {<br>
    const response = await axios.get(url);<br>
    return JSON.stringify(response.data.train_list);<br>
  } catch (error) {<br>
    throw error;<br>
  }<br>
};<br>
//
