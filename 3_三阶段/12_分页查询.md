# 分页查询

在要查询的数据量大的情况下，一次性查询所有数据会导致：

* java内存容器不足以存储这些数据
* 前台一次性显示所有数据不利于阅读

所以出现了分页技术，对查询结果进行分页，一次只提供查询结果的指定内容

mysql的分页查询方言为

`limit start,step`

放到查询语句的最后，以实行分页

# 手动实现分页

需要实现：

* bean:加入分页需要的属性：当前页，分页起始，分页步长

* dao: 在sql语句中加入分页方言语句
* service：传入的实体类中需要包含有分页起始，分页步长

* controller:需要从前端接收当前页与每页条数，并计算数据量，得出总页数并传递给前端

# mybatis分页插件pageHelper

pageHelper为mybatis提供了分页功能，在mybatis的SqlSessionFactory生成SqlSession时，为指定的查询提供了分页，并返回分页需要的前端信息

## maven依赖

5.0以上的版本才提供自动为不同的数据库提供分页方言

~~~xml
<!-- 添加分布插件的包pagehelper -->
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>5.1.1</version>
</dependency>
~~~

## 在spring中配置

在spring配置SqlSessionFactory时，为其配置pageHelper插件：

~~~xml
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="myDataSource"/>
    <property name="configLocation" value="classpath:mybatis.xml"/>
    <!--配置pageHelper插件-->
    <property name="plugins">
        <array>
            <bean class="com.github.pagehelper.PageInterceptor">
                <property name="properties">
                    <value>
                        offsetAsPageNum=true
                        rowBoundsWithCount=true
                        pageSizeZero=true
                        reasonable=true
                    </value>
                </property>
            </bean>
        </array>
    </property>
</bean>
~~~

# 使用pageHeler

* 必须紧靠着查询语句执行之前，声明开启分页
* 查询完毕后，将结果交给pageInfo，能得到所有的分页信息，以便交给前端

~~~java
//service层
@Override
public List<Employee> selectEmps(Employee employee) {
    try {
        //开始分页
        PageHelper.startPage(employee.getPageNumber(),employee.getPageSize());
        //分页后的下一行代码必须执行查询
        return employeeMapper.selectSelective(employee);
    } catch (Exception e) {
        e.printStackTrace();
    }
    return null;
}
//controller层
@RequestMapping("/selectEmps.action")
public String selectEmps(Employee employee ,HttpServletRequest request){
    List<Employee> employees = empService.selectEmps(employee);
    //通过查询结果，pageHelper生成所有分页信息
    PageInfo pageInfo = new PageInfo(employees);
	//将数据与分页信息交给前端
    request.setAttribute("employees",employees);
    request.setAttribute("pageInfo",pageInfo);
    //转发跳转到员工界面
    return "page/emp/employee";
}
~~~

## 前端获取pageInfo

~~~jsp
<table class="table table-hover text-center" id="employees">
    <tr>
        <th><input type="checkbox" name="id[]" id="checkall" value="1"/></th>
        <th>编号</th>
        <th>姓名</th>
        <th>工种</th>
        <th>月薪</th>
        <th>入职日期</th>
        <th>所在部门</th>
        <th>照片</th>
        <th>操作</th>
    </tr>
    
    <c:forEach items="${employees}" var="emp">
        <tr class="canClear">
            <td>
                <input type="checkbox" name="id[]" value="1" id="${emp.empNo}" />
            </td>
            <td>${emp.empNo}</td>
            <td>${emp.empName}</td>
            <td>${emp.empJob}</td>
            <td>${emp.empSal}</td>
            <td>${emp.hiredate}</td>
            <td>${emp.deptName}</td>
            <td><img src="${pageContext.request.contextPath}/photo/${emp.empPhoto}" width="60px" height="60px"></td>
            <td>
                <a href="${pageContext.request.contextPath}/updateEmp?number=${emp.empNo}&photo=${emp.empPhoto}" class="btn btn-info"
                   target="right">修改</a>
                <button class="btn btn-warning" onclick="del(${emp.empNo})">删除</button>
            </td>
        </tr>
    </c:forEach>
    <%--导航栏--%>
    <tr class="canClear">
        <td colspan="8">
            <nav aria-label="Page navigation">
                <ul class="pagination">
                    <c:if test="${pageInfo.pageNum !=1}">
                        <li>
                            <a href="${pageContext.request.contextPath}/emp/selectEmps.action?pageNumber=${pageInfo.pageNum-1}${selectCondition}" aria-label="Previous">
                                <span aria-hidden="true">上一页</span>
                            </a>
                        </li>
                    </c:if>

                    <c:forEach items="${pageInfo.navigatepageNums}" var="i">
                        <li><a <c:if test="${i == pageInfo.pageNum}"> style="color:red"</c:if> href="${pageContext.request.contextPath}/emp/selectEmps.action?pageNumber=${i}${selectCondition}">${i}</a></li>
    </c:forEach>

    <c:if test="${pageInfo.pageNum != pageInfo.pages}">
        <li>
            <a href="${pageContext.request.contextPath}/emp/selectEmps.action?pageNumber=${pageInfo.pageNum+1}${selectCondition}" aria-label="Previous">
                <span aria-hidden="true">下一页</span>
            </a>
        </li>
    </c:if>
    </ul>
</nav>
</td>
</tr>
</table>
~~~















