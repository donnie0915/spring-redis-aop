如果你有遇到什么问题可以联系我：hjp222@gmail.com 
     
此项目是实现以aop的形式，以annotion方式在实现方法上添加redis缓存
     
### 注意：
  1.如果用maven打成jar包引入，只需修改一下配置问题<br>
  2.也可将代码copy到您的项目中。但要修改一些代码和配置文件<br>
  3.对象要实现Serializable 不然不能序列化与反序列化<br>
      
### 使用

```
        @ReadThroughAssignCache(namespace="okhjp_user", valueClass =User.class,expireTime = 100)
	@Override
	public User find(@ParameterValueKeyProvider String uid) {
		System.out.println("query from db");
		User user = new User();
		user.setUserId(uid);
		user.setName("donnieGET");
		return user;
	}

	@ReadThroughAssignCache(namespace="okhjp_user", valueClass =User.class)
	@Override
	public User find(@ParameterValueKeyProvider(order = 1) String uid,
					 @ParameterValueKeyProvider(order = 0) String name) {

		System.out.println("query from db by more param");
		User user = new User();
		user.setUserId(uid);
		user.setName(name);
		user.setAge(1);
		return user;
	}

	@ReadThroughAssignCache(namespace="okhjp_user", valueClass =ArrayList.class)
	@Override
	public List<User> list(@ParameterValueKeyProvider String name) {

		System.out.println("list from db by name");
		List<User> users = new ArrayList<>();

		User user = new User();
		user.setUserId("2");
		user.setName(name);
		user.setAge(2);
		users.add(user);

		User user1 = new User();
		user1.setUserId("3");
		user1.setName(name);
		user1.setAge(3);
		users.add(user);

		return users;
	}

	@UpdateThroughAssignCache(namespace="okhjp_user",valueclass =User.class)
	@Override
	public User insert(@ParameterValueKeyProvider User user) {
		System.out.println("insert into db");
		user.setUserId("111");
		user.setName("donnie");
		return user	;
	}

	@DeleteThroughAssignCache(namespace="okhjp_user")
	@Override
	public boolean delete(@ParameterValueKeyProvider String uid) {
		System.out.println("delete from db");

		return true;
	}

	@UpdateThroughAssignCache(namespace="okhjp_user",valueclass =User.class)
	@Override
	public User update(@ParameterValueKeyProvider User vo) {
		System.out.println("update db ");
		return vo;
	}
	
```
        
        

