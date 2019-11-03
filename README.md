# Здесь находятся примеры входных данных в алгоритм VRP
Данные в папке [examples](examples) в формате JSON с следующими полями:
```json 
{
    "Applications": [ ],
    "Parameters": { },
    "Vehicles": [ ],
    "Depots": [ ]
}
```
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
* Type - тип заявки, существуют 4 варианта:
  * Pickup - забор
  * Delivery - доставки
  * PickupAndDelivery - связанные между собой забор и дальнейшая доставка
  * MultiPickupsAndDelivery - связанные между собой несколько заборов и 1 доставка
* ServiceTime - время(в минутах), необходимое водителю для обслуживания заявки(это может быть погрузка или выгрузка товаров)
* Name - уникальный идентификатор
* StartDate - Начало временного окна заявки в котором она может быть обслужена
* EndDate - Конец временного окна заявки в котором она может быть обслужена
* WeightCapacity - Вес заявки
* VolumeCapacity - Объем заявки
* Skills - необходимые навыки для водителя транспорта, который будет обслуживать заявку(Водитель сможет обслужить заявку при наличии соответственных навыков)
* Location - позиция заявки на карте (координатная плоскость)

---
***Детальный пример объекта **Parameters (параметры алгоритма)*****
```json
    {
        "ConsideVolumeConstraint": false,
        "ConsideWeightConstraint": false,
        "ConsiderDepotConstraint": true,
        "ConsiderVehicleLunch": true
    }
```
* ConsideVolumeConstraint - Учитывание объема заявок и объемной вместительности транспорта
* ConsideWeightConstraint - Учитывание веса заявок и весовой вместительности транспорта
* ConsiderDepotConstraint - Учитывание удельной погрузки на складе (колличество транспорта, которое способно погружаться одновременно в единицу времени(у каждого склада может быть разное величина))
* ConsiderVehicleLunch - Учитывание обеденного времени водителя транспорта
---
***Детальный пример объекта в массиве **Vehicles (транспорт)*****
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
* Name - Уникальный идентификатор
* WeightCapacity - Максимальный вес, который способен погрузить транспорта
* VolumeCapacity - Максимальная объем, который способен вместить транспорт
* LunchInfo - Информация по обеденному времени водителя транспорта
* Location - Позиция транспорта на карте
* Skills - Обладаемые навыки водителя
---
***Детальный пример объекта в массиве **Depots (склад)*****
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
* Location - Позиция
* ResourceConstraint - Удельная пропускная способность склада (одновременно могут погружаться 4 водителя в течении 33 минут) 

---
Если заявки имеет тип **PickupAndDelivery**, то то объект в массиве **Applications** имеет следущий вид:
```json
{
      "Type": "PickupAndDelivery",
      "Name": "zHd9UVOXfrf7Qf7b0hf5",
      "WeightCapacity": 16,
      "VolumeCapacity": 38,
      "Pickup": {
          "ServiceTime": 2326,
          "Location": {
            "X": 3331,
            "Y": 2343
          },
          "StartDate": "2019-11-19T20:51:14.029Z",
          "EndDate": "2019-11-20T02:55:03.029Z"
        },
      "Delivery": {
          "ServiceTime": 2150,
          "Location": {
            "X": 9200,
            "Y": 1736
          },
          "StartDate": "2019-11-19T20:51:14.029Z",
          "EndDate": "2019-11-20T02:55:03.029Z"
      },
      "Skills": [
        "d",
        "b",
        "e"
      ]
    } 
```
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
      "Name": "BBRitUebwf7aBIKJYCfR",
      "WeightCapacity": 85,
      "VolumeCapacity": 58,
      "Pickups": [
         {
          "ServiceTime": 697,
          "Location": {
            "X": 1167,
            "Y": 2454
          },
          "StartDate": "2019-11-20T06:20:06.476Z",
          "EndDate": "2019-11-20T10:50:08.476Z"
        },
        {
          "ServiceTime": 3010,
          "Location": {
            "X": 9994,
            "Y": 1658
          },
          "StartDate": "2019-11-20T06:20:06.476Z",
          "EndDate": "2019-11-20T10:50:08.476Z"
        },
        {
          "ServiceTime": 790,
          "Location": {
            "X": 8366,
            "Y": 9311
          },
          "StartDate": "2019-11-20T06:20:06.476Z",
          "EndDate": "2019-11-20T10:50:08.476Z"
        }
      ],
      "Delivery": {
        "ServiceTime": 2066,
        "Location": {
          "X": 8049,
          "Y": 9197
        },
        "StartDate": "2019-11-20T06:20:06.476Z",
        "EndDate": "2019-11-20T10:50:08.476Z"
      },
      "Skills": [
        "e",
        "a"
      ]
    }
```

* Pickups - Список заборов 
* Delivery - Информация о доставке(водитель не может обслужить доставку, минуя хотя бы 1 забор)
---
Для более подробного академического понимания VRP вы можете ознакомиться с ссылками ниже:

* [Первая ссылка](http://neo.lcc.uma.es/vrp/vehicle-routing-problem/)
* [Вторая ссылка](https://medium.com/opex-analytics/opex-101-vehicle-routing-problems-262a173f4214)
* [Третья ссылка](https://developers.google.com/optimization/routing/vrp) 


Если после прочитанного у вас возникли вопросы, то вы можете нажать [сюда](FAQ.md). <br/>Если же и это не помогло, то прошу написать [сюда.](https://t.me/aae4s)