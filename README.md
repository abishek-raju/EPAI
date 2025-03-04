# EPAI



### Contents
[1.time_it](#timeit)  
[2.squared_power_list](#squaredpowerlist)
[3.polygon_area](#polygonarea)
[4.temp_converter](#tempconverter)
[5.speed_converter](#speedconverter)
[6.test cases](#testcases)
**1.time_it:**<a name="timeit"></a>
```python
def time_it(fn, *args, repetitons=1, **kwargs):
    if repetitons < 0:
        raise ValueError(f"repetitons cannot be less than zero")
    start_time = time.perf_counter()

    for i in range(repetitons):
        fn(*args, **kwargs)

    return time.perf_counter()-start_time
```
Function takes input as another function and executes the same function for repetitions times and calculates the total time taken.
If the repetitions is less than zero ValueError is raised

**2.squared_power_list:**<a name="squaredpowerlist"></a>
```python
def squared_power_list(num,*,start=0, end=5):
    return [num**i for i in range(start,end+1)]
```
Functions takes the power(num) to which the number has to be raised,also  using the range function which also uses the start and end values.
Some Examples:
```python
In[36]:squared_power_list(3,start=0, end=5)
Out[36]: [1, 3, 9, 27, 81, 243]

In[37]:squared_power_list(2,start=0, end=5)
Out[37]: [1, 2, 4, 8, 16, 32]
``` 
**3.polygon_area:**<a name="polygonarea"></a>
```python
def polygon_area(side_length,*,sides):
    sqrt_3 = math.sqrt(3)
    if sides not in area.keys():
        raise ValueError("sides not valid")
    area = {3:(sqrt_3/4)*(side_length**2),
            4:side_length**2,
            5:(1/4)*math.sqrt(5*(5+(2*math.sqrt(5))))*(side_length**2),
            6:(3/2)*sqrt_3*(side_length**2)}
    return area[sides]
```
Function takes the length of a polygon as an input and the number of sides the polygon has and computes the area of the respective polygon. One important point to note here is all the side length's are assumed to be of same.

**4.temp_converter:**<a name="tempconverter"></a>
```python
def temp_converter(temp,*,temp_given_in):
    if temp_given_in =="c":
        return (temp*(9/5)) + 32
    elif temp_given_in == "f":
        return (temp - 32)*(5/9)
    else:
        raise ValueError("temp_given_in not valid")
```
Function takes the temperature given in either celsius("c") or fahrenhiet("f") converts to the other.

**5.speed_converter:**<a name="speedconverter"></a>
```python
def speed_converter(speed,*,dist,time):
    km_conv = {"km":1,"m":1000,"ft":3280,"yrd":1093}
    time_conv = {"hr":1,"day":0.0416667,"m":60,"s":3600,"ms":3600000}
    if (dist not in km_conv.keys()) or (time not in time_conv.keys()):
        raise ValueError("dist or time units invalid")
    return speed*(km_conv[dist]/time_conv[time])

```
Here the speed from the user is assumed to be in "kmph".So to convert the length from "km" to any one of "km/m/ft/yrd" measure's we just have to **multiply** the given value with the length conversion factor.
Similarly to convert the speed from "per hour" measure to one of "ms/s/m/hr/day" we have to **divide** the given value with the time conversion factor.

**5.test cases:**<a name="testcases"></a>
```python
CHECK_FOR_FUNCT_IMPL = ["time_it",
                        "squared_power_list",
                        "polygon_area",
                        "temp_converter",
                        "speed_converter"
                        ]


README_CONTENT_CHECK_FOR = ["time_it",
                        "squared_power_list",
                        "polygon_area",
                        "temp_converter",
                        "speed_converter"
                        ]


# Tests related to readme
def test_readme_exists():
    assert os.path.isfile("README.md"), "README.md file missing!"


def test_readme_contents():
    readme = open("README.md", "r", encoding="utf-8")
    readme_words = readme.read().split()
    readme.close()
    assert len(
        readme_words) >= 500, "Make your README.md file interesting! Add atleast 500 words"


def test_readme_proper_description():
    READMELOOKSGOOD = True
    f = open("README.md", "r", encoding="utf-8")
    content = f.read()
    f.close()
    for c in README_CONTENT_CHECK_FOR:
        if c not in content:
            print(c)
            READMELOOKSGOOD = False
            pass
    assert READMELOOKSGOOD, "You have not described all the functions/class well in your README.md file"


def test_readme_file_for_formatting():
    f = open("README.md", "r", encoding="utf-8")
    content = f.read()
    f.close()
    assert content.count("#") >= 10, "Readme is not formatted properly"


def test_indentations():
    ''' Returns pass if used four spaces for each level of syntactically \
    significant indenting.'''
    lines = inspect.getsource(program)
    spaces = re.findall('\n +.', lines)
    for count,space in enumerate(spaces):
        print(count,space)
        assert len(space) % 4 == 2, "Your script contains misplaced indentations"
        assert len(re.sub(r'[^ ]', '', space)) % 4 == 0, "Your code indentation does not follow PEP8 guidelines"


def test_function_name_had_cap_letter():
    functions = inspect.getmembers(program, inspect.isfunction)
    for function in functions:
        print(function)
        assert len(re.findall(
            '([A-Z])', function[0])) == 0, "You have used Capital letter(s) in your function names"

def test_function_count():
    functions = inspect.getmembers(test_session, inspect.isfunction)
    assert len(functions) > 20, 'Test cases seems to be low. Work harder man...'


def test_function_repeatations():
    functions = inspect.getmembers(test_session, inspect.isfunction)
    names = []
    for function in functions:
        names.append(function)
    assert len(names) == len(set(names)), 'Test cases seems to be repeating...'


def test_time_it_for_valueerror():
    with pytest.raises(ValueError):
        program.time_it(print,repetitons = -1)


def test_time_it_for_typeerror():
    i = 0
    with pytest.raises(TypeError):
        program.time_it(i,repetitons = 1)

def test_squared_power_list():
    output = program.squared_power_list(2, start=0, end=5)
    assert set(output) == set([1, 2, 4, 8, 16, 32])

def test_polygon_area_triangle():
    assert math.isclose(program.polygon_area(2,sides = 3), 1.73 ,abs_tol=0.1)
     
def test_polygon_area_rectangle():
    assert math.isclose(program.polygon_area(2,sides = 4), 4 ,abs_tol=0.1)
     
def test_polygon_area_pentagon():
    assert math.isclose(program.polygon_area(2,sides = 5), 6.88191 ,abs_tol=0.1)

def test_polygon_area_hexagon():
    assert math.isclose(program.polygon_area(2,sides = 6), 10.39 ,abs_tol=0.1)

def test_polygon_area_for_valueerror():
    with pytest.raises(ValueError):
        program.polygon_area(2,sides = 7)

def test_temp_converter_c_to_f():
    assert math.isclose(program.temp_converter(0,temp_given_in = "c"),32.0)

def test_temp_converter_f_to_c():
    assert math.isclose(program.temp_converter(32,temp_given_in = "f"),0)

def test_temp_converter_valueerror():
    with pytest.raises(ValueError):
        program.temp_converter(32,temp_given_in = "g")

def test_temp_converter_typeerror():
    with pytest.raises(TypeError):
        program.temp_converter("a",temp_given_in = "f")

def test_speed_converter_valueerror():
    with pytest.raises(ValueError):
        program.speed_converter(speed = 100,dist = "mp",time = "s")

def test_speed_converter_kmph_mph():
    math.isclose(program.speed_converter(speed = 100,dist = "m",time = "hr"),100000.0)

def test_speed_converter_kmph_kmps():
    math.isclose(program.speed_converter(speed = 100,dist = "km",time = "s"),0.02777777777)

def test_speed_converter_kmph_kmpday():
    math.isclose(program.speed_converter(speed = 100,dist = "km",time = "day"),2399.998)
    
def test_speed_converter_typeerror():
    with pytest.raises(TypeError):
        program.speed_converter(speed = "a",dist = "m",time = "s")
```