
# Application Information

| App ID               | F5445                                                    |
| -------------------- | -------------------------------------------------------- |
| App Title            | Analyze and Resolve Blocked Documents - Trade Compliance |
| OData Service(s)     | SLL_BLKTRDCMPDOC_ANALYZE                                 |
| SEGW Gateway Project | ?

# Approach 1 (Not perfect but it works most of the time)

## ADT: Ctrl + Shift + A

Delete few characters of the service from right until a Gateway Project is found.

![image](https://github.com/zzvikesh/index/assets/167571098/d8c4082a-8d83-4f45-b923-3a946ea9f627)

## Transaction Code: SEGW

Check the service under Runtime Artifacts.

![image (1)](https://github.com/zzvikesh/index/assets/167571098/d20ceef3-a59b-4c75-8fc3-f60e7afff385)

Service is not matching with our the service listed on Fiori App Library. 

# Approach 2 

## Transaction Code: /IWFND/MAINT_SERVICE

![image (2)](https://github.com/zzvikesh/index/assets/167571098/e6d8035b-d503-4b79-aa6d-da8ab939cd8d)

Execute Gateway client.

![image (3)](https://github.com/zzvikesh/index/assets/167571098/edec96e1-39af-44c4-91bd-13aaeaf689fb)

Check Service Implementation.

> We can directly execute Gateway Client using Transaction Code `/IWFND/GW_CLIENT` and then manually giving the Service Name form Fiori App Library.

![image (4)](https://github.com/zzvikesh/index/assets/167571098/4861184c-2139-4024-b9c3-d6e89f3c7c13)

![image (5)](https://github.com/zzvikesh/index/assets/167571098/9d72ff5d-30d9-4bb1-8246-8d6bc1f504e0)

Find the package of the class.

![image (6)](https://github.com/zzvikesh/index/assets/167571098/5b6a22a2-81e4-4139-afe6-97db5f88c063)

Load all the contents of the package, to find the Gateway Project.

![image (7)](https://github.com/zzvikesh/index/assets/167571098/cd6b852b-bad6-4780-ad30-ad041d0feb0c)

Service of Gateway Project is matching with Service Listed in Fiori Application Library.

![image (8)](https://github.com/zzvikesh/index/assets/167571098/dcd47963-82d8-4a25-94d5-3d8db8d3f898)
