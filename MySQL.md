# MySQL

Oracle 다음으로 가장 많이 사용되는 관계형 DB이다. **무료**이기 때문에 웹 개발에서 많은 개발자들이 이용하고 있다. 점유율 면에선 Oracle에 비교해 비슷한 수준으로 1,2위를 다투고 있다. Bitnami를 이용해 MySQL을 실습한다.

SQL은 **S**tructured **Q**uery **L**anguage의 약자이다. 구조화된 쿼리 언어라는 뜻이다. 사용자의 요청(쿼리)에 따라 해당 명령을 수행한다.

![mysql](https://user-images.githubusercontent.com/52786355/84627309-ab3e7480-af21-11ea-9c71-061dbde8f5f5.PNG)

<center>[데이터 베이스 구조]</center>

하나의 DB 서버 안에 여러 DB(스키마)가 존재하고, 해당 스키마 안에 여러 테이블이 존재한다. 

```mysql
SELECT
    [ALL | DISTINCT | DISTINCTROW ]
    [HIGH_PRIORITY]
    [STRAIGHT_JOIN]
    [SQL_SMALL_RESULT] [SQL_BIG_RESULT] [SQL_BUFFER_RESULT]
    [SQL_CACHE | SQL_NO_CACHE] [SQL_CALC_FOUND_ROWS]
    select_expr [, select_expr] ...
    [into_option]
    [FROM table_references
      [PARTITION partition_list]]
    [WHERE where_condition]
    [GROUP BY {col_name | expr | position}
      [ASC | DESC], ... [WITH ROLLUP]]
    [HAVING where_condition]
    [ORDER BY {col_name | expr | position}
      [ASC | DESC], ...]
    [LIMIT {[offset,] row_count | row_count OFFSET offset}]
    [PROCEDURE procedure_name(argument_list)]
    [into_option]
    [FOR UPDATE | LOCK IN SHARE MODE]

into_option: {
    INTO OUTFILE 'file_name'
        [CHARACTER SET charset_name]
        export_options
  | INTO DUMPFILE 'file_name'
  | INTO var_name [, var_name] ...
}
```

과 [MySQL Cheat Sheet](https://www.zentut.com/wp-content/uploads/2012/10/sqlcheatsheet.jpg)와 함께라면 어떤 명령도 입력할 수 있다. (~~사실 없어도 검색하면 된다.~~)



## Index

- [Join](#Join)





## Join

![mysql2](https://user-images.githubusercontent.com/52786355/84632774-5b17e000-af2a-11ea-8636-558648481023.PNG)

<center>[Join의 종류]</center>

Join의 모든 것을 사진 하나로 알 수 있다. 자신이 뽑고자 하는 모든 경우의 수는 벤 다이어그램으로 나타낼 수 있고, 경우마다 LEFT JOIN, RIGHT JOIN, INNER JOIN, FULL OUTER JOIN, IS NULL 등의 조건을 부여해  뽑아낼 수 있다. 일반적으로 INNER JOIN이 성능이 좋다고 한다.









