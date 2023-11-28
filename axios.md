## // component
```js
//
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
//

// api using axios #########################################################################################
//  
import axios from 'axios';

export const RequestMap = async (url) => {
  try {
    const response = await axios.get(url);
    return JSON.stringify(response.data.train_list);
  } catch (error) 
    throw error;
  }
};
//
// Finally success code  ##############################################################################################

```js
//
import axios from 'axios';
import { useContext, useEffect } from 'react';
import { Context } from '../context/Context';

export const RequestMap = (url) => {
    const { setActiveIndicator, setErrorIndicator, setData, setFullData, setErrorMessage } = useContext(Context);
    useEffect(() => {
        async function fetchData() {
            try {
                setActiveIndicator(true);
                const response = await axios(url);
                const json = response.data.train_list;
                setData(json);
                setFullData(json);
            } catch (error) {
                setErrorIndicator(true);
                setErrorMessage(error.toString());
            } finally {
                setActiveIndicator(false);
                setErrorIndicator(false);
            }
        }
        fetchData();
    }, [url]);

}
//


