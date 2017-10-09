# Angular+ Best Practices
## 1 - Oh not!! OVER_QUERY_LIMIT on Google API!
* This tips can use on Angular/Ionic

Do not worry about this, the servers of Google are simply preventing of one attack the Deny of Service or that many requisitions
per second overload your servers. But how do you can coding and deal this error?

Let's take a look an following exemple:

```typescript
@Component({
  selector: 'page-location',
  templateUrl: 'location.html'
})
export class LocationPage {
  private VALUE_FINDING_ADDRESS = 'Identificando endereço ...';

  public geocoder: google.maps.Geocoder;
  public myLocation: google.maps.LatLng;
  public placeholderLocation: string;
 
  private getPlaceholderLocation() {
    this.placeholderLocation = this.VALUE_FINDING_ADDRESS;
    this.geocoder.geocode({
      location: this.myLocation
    }, 
    (result, status) => {
      if(status === google.maps.GeocoderStatus.OK) {
        result[0].address_components.forEach((addressComp) => {
          if(addressComp.types[0] === 'route') {
            this.placeholderLocation = addressComp.long_name;
          }
        });
      } else {
        this.placeholderLocation = '';
      }
    });
}
```
* The above code we use the method geocode from google.maps.Geocoder to get the address information as route, city ...
  given an position lat lng. The second param on CallBack is the **status** of requisitions the can give us if a request is 'OK'
  or 'OVER_QUERY_LIMIT', to check more values to status visit:
  [GeocodingStatusCodes](https://developers.google.com/maps/documentation/javascript/geocoding#GeocodingStatusCode)
  Well this case above, if the server return one status of 'OVER_QUERY_LIMIT' nothing will come pass and the user will not see
  the address, but there an way to handle the error 'OVER_QUERY_LIMIT', see the code following:

```typescript
@Component({
  selector: 'page-location',
  templateUrl: 'location.html'
})
export class LocationPage {
  private VALUE_FINDING_ADDRESS = 'Identificando endereço ...';

  public geocoder: google.maps.Geocoder;
  public myLocation: google.maps.LatLng;
  public placeholderLocation: string;
 
  private getPlaceholderLocation() {
    this.placeholderLocation = this.VALUE_FINDING_ADDRESS;
    this.geocoder.geocode({
      location: this.myLocation
    }, 
    (result, status) => {
      if(status === google.maps.GeocoderStatus.OK) {
        result[0].address_components.forEach((addressComp) => {
          if(addressComp.types[0] === 'route') {
            this.placeholderLocation = addressComp.long_name;
          }
        });
      } else if(status === google.maps.GeocoderStatus.OVER_QUERY_LIMIT) {
        setTimeout(() => this.getPlaceholderLocation(), 3000);
      } else {
        this.placeholderLocation = '';
      }
    });
}
```
* The above code get the status if one OVER_QUERY_LIMIT is returned by server, then we will wait 3 seconds and trying again until
  receive status 'OK', this practice is recommended by [Doc Google - Usage Limits](https://developers.google.com/maps/premium/previous-licenses/articles/usage-limits).

  You also can increment these implematation, making the number limit of try, or the milleseconds is increase as the try is became
  higher.
  
Thanks and see you soon. Any question or suggestion, open one issue.

## 2 - Comming Soon:
