# Здесь находятся примеры входных данных в алгоритм VRP
Любой из примеров имеет формат JSON с следующими полями:
```json 
{
    "Applications": [ 
       
    ],
    "Parameters": {
        
    },
    "Vehicles": [
        
    ],
    "Depots": [
        
    ]
}
```
где
* Applications - массив заявок
* Parameters - параметры алгоритма
* Vehicles - массив водителей
* Depots - массив складов

---
***Детальный пример объекта в массиве **Applications(заявки)*****
```json 
 {
      "ServiceTime": 360,
      "Type": "Pickup",
      "Name": "yOzexygIb5HW1PhbGf4B",
      "StartDate": "2019-11-19T22:16:06.684Z",
      "EndDate": "2019-11-20T06:26:26.684Z",
      "WeightCapacity": 95,
      "VolumeCapacity": 84,
      "Skills": [
          "c",
          "e"
      ],
      "Location": {
          "X": 4891,
          "Y": 6361
      }
}
```
***Описание полей***

* Type - тип, существуют 4 варианта:
  * Pickup - забор
  * Delivery - доставки
  * PickupAndDelivery - связанные между собой забор и дальнейшая доставка
  * MultiPickupsAndDelivery - связанные между собой несколько заборов и 1 доставка
* ServiceTime - время(в минутах) необходимое водителю для обслуживания заявки
* Name - уникальный идентификатор
* StartDate - Начало временного окна заявки в котором она может быть обслужена
* EndDate - Конец временного окна заявки в котором она может быть обслужена
* WeightCapacity - Вес заявки
* VolumeCapacity - Объем заявки
* Skills - необходимые навыки для транспорта, который будет обслуживать заявку(Водитель сможет обслужить заявку при наличии соответственных навыков)
* Location - позиция заявки на карте (координатная плоскость)

---
***Детальный пример объекта **Parameters(параметры алгоритма)*****
```json
    {
        "ConsideVolumeConstraint": false,
        "ConsideWeightConstraint": false,
        "ConsiderDepotConstraint": true,
        "ConsiderVehicleLunch": true
    }
```

***Описание полей***
* ConsideVolumeConstraint - Учитывание объема заявок и объемной вместительности транспорта
* ConsideWeightConstraint - Учитывание веса заявок и весовой вместительности транспорта
* ConsiderDepotConstraint - Учитывание удельной погрузки на складе (колличество транспорта, которое способно погрузижаться одновременно в единицу времени)
* ConsiderVehicleLunch - Учитывание обеденного времене водителя транспорта
---
***Детальный пример объекта в массиве **Vehicles(транспорт)*****
```json
    {
        "Name": "Jp93oPp2Wk5fD2eP3jyu",
        "WeightCapacity": 860,
        "VolumeCapacity": 1003,
        "LunchInfo": {
            "Start": "12:00",
            "End": "13:30"
        },
        "Location": {
            "X": 5121,
            "Y": 8067
        },
        "Skills": [
            "b",
            "a",
            "d"
        ]
    }
```

***Описание полей***
* Name - Уникальный идентификатор водителя
* WeightCapacity - Максимальный вес, который способен погрузить транспорта
* VolumeCapacity - Максимальная объем, который способен вместить транспорт
* LunchInfo - Информация по обеденному времени водителя транспорта
* Location - Позиция водителя на карте
* Skills - Обладаемые навыки данного водителя водителя

***Детальный пример объекта в массиве **Depots(склады)*****
```json
    {
        "Location": {
            "X": 990,
            "Y": 66
        },
        "ResourceConstraint": {
            "VehiclesUnit": 4,
            "MinutesUnit": 33
        }
    }
```
***Описание полей***
* Location - Позиция
* ResourceConstraint - Удельная пропускная способность склада (одновременно могут погружаться 4 водителя за 33 минуты) 


---
Если заявки имеет тип **PickupAndDelivery**, то то объект в массиве **Applications** имеет следущий вид:
```json
{
      "Type": "PickupAndDelivery",
      "ServiceTime": 360,
      "Name": "zHd9UVOXfrf7Qf7b0hf5",
      "WeightCapacity": 16,
      "VolumeCapacity": 38,
      "Pickup": {
        "Location": {
          "X": 5637,
          "Y": 7153
        },
        "StartDate": "2019-11-20T14:41:39.504Z",
        "EndDate": "2019-11-21T02:10:15.504Z"
      },
      "Delivery": {
        "Location": {
          "X": 6684,
          "Y": 41
        },
        "StartDate": "2019-11-20T14:41:39.504Z",
        "EndDate": "2019-11-21T02:10:15.504Z"
      },
      "Skills": [
        "d",
        "b",
        "e"
      ]
    } 
```
где:
* Pickup - Информация по забору 
    * Location - Позиция забора
    * StartDate, EndDate - Временное окно забора
* Delivery - Информация по доставке 
    * Location - Позиция доставки
    * StartDate, EndDate - Временное окно доставки

---
Если заявки имеет тип **MultiPickupsAndDelivery**, то объект в массиве **Applications** имеет следущий вид:
```json
{
      "Type": "MultiPickupsAndDelivery",
      "ServiceTime": 360,
      "Name": "BBRitUebwf7aBIKJYCfR",
      "WeightCapacity": 85,
      "VolumeCapacity": 58,
      "Pickups": [
        {
          "Location": {
            "X": 4822,
            "Y": 7564
          },
          "StartDate": "2019-11-20T10:28:46.784Z",
          "EndDate": "2019-11-20T18:04:04.784Z"
        },
        {
          "Location": {
            "X": 695,
            "Y": 7825
          },
          "StartDate": "2019-11-20T10:28:46.784Z",
          "EndDate": "2019-11-20T18:04:04.784Z"
        },
        {
          "Location": {
            "X": 5872,
            "Y": 8954
          },
          "StartDate": "2019-11-20T10:28:46.784Z",
          "EndDate": "2019-11-20T18:04:04.784Z"
        },
        {
          "Location": {
            "X": 4296,
            "Y": 294
          },
          "StartDate": "2019-11-20T10:28:46.784Z",
          "EndDate": "2019-11-20T18:04:04.784Z"
        }
      ],
      "Delivery": {
        "Location": {
          "X": 7703,
          "Y": 233
        },
        "StartDate": "2019-11-20T10:28:46.784Z",
        "EndDate": "2019-11-20T18:04:04.784Z"
      },
      "Skills": [
        "e",
        "a"
      ]
    }
```
где:
* Pickups - Список заборов 
* Delivery - Информация о доставке(водитель не может обслужить доставку, минуя хотя бы 1 забор)

Если после прочитанного у вас возникли вопросы, то вы можете нажать [сюда](FAQ.md). Если же и это не помогло, то прошу написать [сюда](https://t.me/aae4s)