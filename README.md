# Icook

## 代码篇 （Go）


## 数据库篇（MariaDB）
1.创建表 3个
    -- 创建菜谱表
    CREATE TABLE recipes (
        id INT PRIMARY KEY,
        name VARCHAR(255),
        cover_image VARCHAR(255),
        video_link VARCHAR(255),
    );

    -- 创建标签表
    CREATE TABLE tags (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(50) NOT NULL UNIQUE
    );

    -- 创建菜谱标签关联表
    CREATE TABLE recipe_tags (
        recipe_id INT,
        tag_id INT,
        FOREIGN KEY (recipe_id) REFERENCES recipes(id) ON DELETE CASCADE,
        FOREIGN KEY (tag_id) REFERENCES tags(id) ON DELETE CASCADE,
        PRIMARY KEY (recipe_id, tag_id)
    );

2.在excel中编辑好需要的数据，保存为csv文件，再通过命令导入到数据库里去。
    类似下方==>
        LOAD DATA INFILE 'recipes.csv'
        INTO TABLE recipes
        FIELDS TERMINATED BY ',' 
        ENCLOSED BY '"'
        LINES TERMINATED BY '\n'
        IGNORE 1 ROWS
        (id, name, cover_image, video_link);

