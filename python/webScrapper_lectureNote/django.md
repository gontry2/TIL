# Django

* Instargram, pinterest
* arguments (`*args`) => tuple, keyword arguments (`**kwargs`)  => dictionary
* OOP : blueprint(class) -> object(instance)
  * Class has attributes(properties) and methods(function).
  * Python always has 'self' argument which is the first argument of every method.

```python
# basic
class Car():
    
    def __init__(self, **kwargs):
        self.wheels = 4
        self.doors = 4
        self.color = kwargs.get("color", "black")
        self.price = kwargs.get("price", "$20")
        
    def __str__(self):
        return f"Car with {self.wheels} wheels"
    
    
porche = Car(color="green", price="$40")
print(porche.color, porche.price)
>> green $40
```



```python
# extend(inherit)
class Car():
    
    def __init__(self, **kwargs):
        self.wheels = 4
        self.doors = 4
        self.color = kwargs.get("color", "black")
        self.price = kwargs.get("price", "$20")
        
    def __str__(self):
        return f"Car with {self.wheels} wheels"
    
class Convertible(Car):
	
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.time = kwargs.get("time", 10)
    
    def take_off(self):
        return "taking off"
    
    # overriding
    def __str__(self):
        return "Car with no roof"

class SomethingElse(Convertible):
    pass

porche = Convertible(color="green", price="$40")
porche.take_off()
>> taking off
```



출처: [노마드 아카데미(Python으로 웹 스크래퍼 만들기)](https://nomadcoders.co/python-for-beginners/lobby)

