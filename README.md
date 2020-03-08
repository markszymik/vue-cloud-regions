
# Vue cloud provider regions select  
  
Simple HTML `<select>` with cloud provider list regions.

## Install  
```  
npm install vue-cloud-regions
```  
### Usage  
  
 #### Basic
```  
<CloudRegionsSelect provider="aws" />  
```  

#### Exclude regions

```  
<CloudRegionsSelect provider="aws" exclude="['us-west-1','us-west-2']" />  
```  
#### Include regions

```  
<CloudRegionsSelect provider="aws" include="['eu-west-1']" />  
```  

### Providers

|Provider| Code  |
|--|--|
| Amazon Web Services (AWS) | `aws` |
| Google Cloud Platform | `gcp` |
| Digital Ocean | `do` |

  
## Author  
  
Mark Szymik  
  
## License  
  
MIT