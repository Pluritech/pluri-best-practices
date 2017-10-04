# Ionic - Best Practices

## 1 - When you work with Dates in apps that will run on IOs:
- If a date is returned by server as like as "2017-10-02 17:00" you should always replace the dash to bar before the new Date as follow:

```typescript
let value = '2017-10-02 17:00';
new Date(value.replace(/-/g, '/'));
//Mon Oct 02 2017 17:00:00 GMT-0300 (BRT)
```

This way can prevent an error in Safari/IOs who recognize as date invalid when has dash separator.


## 2 - Comming Soon:
