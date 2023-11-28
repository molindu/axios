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
# Finally success code 

import axios from 'axios';<br>
import { useContext, useEffect } from 'react';<br>
import { Context } from '../context/Context';<br>
<br>
export const RequestMap = (url) => {<br>
    const { setIsLoading, setActiveIndicator, setErrorIndicator, setError, error, setData, setFullData, isLoading, setLoadingMessage, setErrorMessage } = useContext(Context);<br>
    useEffect(() => {<br>
        async function fetchData() {<br>
            try {<br>
                setIsLoading(true);<br>
                const response = await axios(url);<br>
                const json = response.data.train_list;<br>
                console.log(json);<br>
                setData(json);<br>
                setFullData(json);<br>
            } catch (error) {<br>
                setError(error.toString());<br>
            } finally {<br>
                if (error) {<br>
                    setErrorIndicator(true);<br>
                    setErrorMessage(error);<br>
                }<br>
                if (isLoading) {<br>
                    setActiveIndicator(true);<br>
                    setLoadingMessage('Loding Train Details ...');<br>
                }<br>
                setIsLoading(false);<br>
                setActiveIndicator(false);<br>
                setErrorIndicator(false);<br>
            }<br>
        }<br>
        fetchData();<br>
    }, [url]);<br>
}<br>

