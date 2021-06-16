# 动态SQL

### choose

```xml
<where>
    <choose>
        <when test="title!=null">
            title=#{title}
        </when>
        <when test="author!=null">
            author=#{author}
        </when>
        <otherwise>
            views=#{views}
        </otherwise>
    </choose>
</where>
```

### set

```xml
<update id="updateBlog" parameterType="map">
    update blog
    <set>
        <if test="title!=null">
            title=#{title},
        </if>
        <if test="author!=null">
            author=#{author},
        </if>
        <if test="views!=null">
            views=#{views},
        </if>
    </set>
    where id=#{id}
</update>
```
