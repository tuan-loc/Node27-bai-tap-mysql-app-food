CREATE DATABASE db_app_food;

USE db_app_food;

CREATE TABLE food_type(
	type_id INT PRIMARY KEY AUTO_INCREMENT,
    type_name VARCHAR(255)
);

CREATE TABLE food(
	food_id INT PRIMARY KEY AUTO_INCREMENT,
    food_name VARCHAR(255),
    image VARCHAR(255),
    price FLOAT,
    descs VARCHAR(255),
    type_id INT,

	FOREIGN KEY (type_id) REFERENCES food_type(type_id)
);

CREATE TABLE sub_food(
	sub_id INT PRIMARY KEY AUTO_INCREMENT,
    sub_name VARCHAR(255),
    sub_price FLOAT,
    food_id INT,
    
    FOREIGN KEY (food_id) REFERENCES food(food_id)
);

CREATE TABLE users(
	user_id INT PRIMARY KEY AUTO_INCREMENT,
    full_name VARCHAR(255),
    email VARCHAR(255),
    pass_word VARCHAR(255)
);

CREATE TABLE orders(
	user_id INT,
    food_id INT,
    amount INT,
    code VARCHAR(255),
    arr_sub_id VARCHAR(255),
    
    PRIMARY KEY(user_id, food_id),
    FOREIGN KEY (user_id) REFERENCES users(user_id),
    FOREIGN KEY (food_id) REFERENCES food(food_id)
);

CREATE TABLE restaurant(
	res_id INT PRIMARY KEY AUTO_INCREMENT,
    res_name VARCHAR(255),
    image VARCHAR(255),
    descs VARCHAR(255)
);

CREATE TABLE rate_res(
	user_id INT,
    res_id INT,
    amount INT,
    date_rate DATETIME,
    
    PRIMARY KEY(user_id, res_id),
    FOREIGN KEY(user_id) REFERENCES users(user_id),
    FOREIGN KEY(res_id) REFERENCES restaurant(res_id)
);

CREATE TABLE like_res(
	user_id INT,
    res_id INT,
    date_like DATETIME,
    
    PRIMARY KEY(user_id, res_id),
    FOREIGN KEY(user_id) REFERENCES users(user_id),
    FOREIGN KEY(res_id) REFERENCES restaurant(res_id)
);

INSERT INTO food_type(type_id, type_name) VALUES
(1, 'Đồ uống'),
(2, 'Thức ăn nhanh'),
(3, 'Món nước'),
(4, 'Ăn vặt'),
(5, 'Món chay');

INSERT INTO food (food_id, food_name, image, price, descs, type_id) VALUES
(1, 'Coke', 'https://cdn.tgdd.vn/Products/Images/2443/83757/bhx/nuoc-ngot-coca-cola-lon-235ml-202211252238192839.jpg', 5, 'coca cola', 1),
(2, 'Heniken', 'https://biaruoungoainhap.com/wp-content/uploads/2019/04/15391018745886.jpg', 10, 'đây là bia', 1),
(3, 'Burger', 'https://burgerking.vn/media/catalog/product/cache/1/image/1800x/040ec09b1e35df139433887a97daa66f/c/r/crunchy_whp-min_1.jpg', 7, 'hum bơ gơ', 2),
(4, 'Hủ tiếu', 'https://daubepgiadinh.vn/wp-content/uploads/2018/05/hinh-hu-tiu-nam-vang.jpg', 30, 'hủ tiếu gõ', 3),
(5, 'Bún bò', 'https://i.ytimg.com/vi/A_o2qfaTgKs/maxresdefault.jpg', 50, 'bún bòa', 3),
(6, 'Khoai tây chiên', 'http://icdn.dantri.com.vn/zoom/1200_630/2017/khoai-tay-chien-1497363342895.jpg', 100, 'potato', 2),
(7, 'Sandwich', 'https://monngonmoingay.com/wp-content/uploads/2020/12/sandwich-kep-cha-tom-500.jpg', 2, 'san quýt', 2),
(8, 'Đồ chay', 'https://cdn.tgdd.vn/Files/2022/03/21/1421421/tong-hop-16-cach-lam-mon-chay-thanh-dam-dinh-duong-tai-nha-202203211050443101.jpg', 1, 'đây là đồ ăn chay', 5),
(9, 'Bánh tráng', 'https://res.klook.com/image/upload/q_85/c_fill,w_750/v1596008298/blog/eibedalo0wncojkerkpg.jpg', 33, 'bánh cháng', 4),
(10, 'xúc xích', 'https://www.tvpfood.com/image/cache/catalog/product/san-pham-xien-que-tiec/xuc-xich-berlin-03-1024x1024.png', 22, 'sút sít', 4);

INSERT INTO sub_food(sub_id, sub_name, sub_price, food_id) VALUES
(1, 'Hành phi', 1, 4),
(2, 'Hành phi', 1, 5),
(3, 'Hành phi', 1, 8),
(4, 'Trân châu', 2, 1),
(5, 'Trân châu', 2, 2),
(6, 'Tương ớt', 3, 3),
(7, 'Tương ớt', 3, 10),
(8, 'Tương ớt', 3, 4),
(9, 'Tương ớt', 3, 5),
(10, 'Hành phi', 1, 5),
(11, 'Tương ớt', 1, 4),
(12, 'Tương ớt', 1, 2),
(13, 'Tương ớt', 1, 6),
(14, 'Tương ớt', 1, 9),
(15, 'Tương ớt', 1, 7);

INSERT INTO users (user_id, full_name, email, pass_word) VALUES
(1, 'Tony', 'tony@gmail.com', '1234'),
(2, 'John wick', 'john@gmail.com', '1234'),
(3, 'Peter', 'pi@gmail.com', '1234'),
(4, 'Kang', 'kang@gmail.com', '1234'),
(5, 'Minh', 'minh@gmail.com', '123456'),
(6, 'Huong', 'huong@gmail.com', '123'),
(7, 'Ngoc', 'Ngoc@gmail.com', 'vgfddbv'),
(8, 'Hulk', 'hulk@gmail.com', '1234'),
(9, 'Thanos', 'thanos@gmail.com', '1234'),
(10, 'Thor', 'thor@gmail.com', '1234');

INSERT INTO orders (user_id, food_id, amount, code, arr_sub_id) VALUES
(1, 1, 3, '', '[1,2]'),
(2, 2, 2, '', '[4,5]'),
(3, 1, 1, '', '[1,3]'),
(4, 4, 1, '', '[1,5]'),
(4, 5, 5, '', '[1,4]'),
(4, 8, 1, '', '[2,5]'),
(6, 5, 10, '', '[1,2,3]'),
(6, 3, 4, '', '[1,4]'),
(6, 2, 4, '', '[4,5]'),
(8, 4, 1, '', '[3,4]'),
(8, 2, 9, '', '[3,7]'),
(9, 8, 5, '', '[3,1]'),
(10, 7, 3, '', '[7,8]'),
(10, 1, 8, '', '[4,6]');

INSERT INTO restaurant(res_id, res_name, image, descs) VALUES
(1, 'Phúc Long', 'https://static.mservice.io/placebrand/s/momo-upload-api-200218150929-637176353692616410.jpg', 'pl'),
(2, 'KFC', '/public/img/1659847246771_test.mp4', 'kfc'),
(3, 'Kichi kichi', 'https://aeonmall-haiphong-lechan.com.vn/wp-content/uploads/2020/09/25.-kichi-kichi.jpg', 'kckc');

INSERT INTO rate_res(user_id, res_id, amount, date_rate) VALUES
(1, 2, 4, '2022-01-01 09:00:00'),
(1, 3, 5, '2022-01-01 09:00:00'),
(2, 1, 3, '2022-01-01 09:00:00'),
(2, 3, 3, '2022-01-01 09:00:00');

INSERT INTO like_res (user_id, res_id, date_like) VALUES
(1, 1, '2022-01-01 09:00:00'),
(1, 2, '2022-01-01 09:00:00'),
(1, 3, '2022-01-01 09:00:00'),
(2, 2, '2022-01-01 09:00:00'),
(8, 1, '2022-01-01 09:00:00'),
(2, 1, '2022-01-01 09:00:00'),
(2, 3, '2022-01-01 09:00:00'),
(10, 1, '2022-01-01 09:00:00'),
(10, 2, '2022-01-01 09:00:00'),
(10, 3, '2022-01-01 09:00:00'),
(9, 1, '2022-01-01 09:00:00'),
(8, 2, '2022-01-01 09:00:00'),
(3, 3, '2022-01-01 09:00:00'),
(3, 1, '2022-01-01 09:00:00'),
(3, 2, '2022-01-01 09:00:00'),
(4, 1, '2022-01-01 09:00:00'),
(4, 2, '2022-01-01 09:00:00'),
(8, 3, '2022-01-01 09:00:00');

SELECT users.full_name, count(*) AS total_like FROM users
LEFT JOIN like_res
ON users.user_id = like_res.user_id
GROUP BY users.full_name
ORDER BY total_like DESC
LIMIT 5;

SELECT restaurant.res_name, count(*) AS total_like FROM restaurant
LEFT JOIN like_res
ON restaurant.res_id = like_res.res_id
GROUP BY restaurant.res_name
ORDER BY total_like DESC
LIMIT 2;

SELECT users.full_name, SUM(amount) AS total_order FROM users
LEFT JOIN orders
ON users.user_id = orders.user_id
GROUP BY users.full_name
ORDER BY total_order DESC
LIMIT 1;

SELECT users.full_name, orders.amount AS orders, like_res.res_id AS likes, rate_res.amount AS rate FROM users
LEFT JOIN orders
ON users.user_id = orders.user_id
LEFT JOIN like_res
ON users.user_id = like_res.user_id
LEFT JOIN rate_res
ON users.user_id = rate_res.user_id
WHERE orders.amount IS NULL AND rate_res.amount IS NULL AND like_res.res_id IS NULL;

SELECT food.food_name, AVG(sub_price) AS average FROM food
LEFT JOIN sub_food
ON food.food_id = sub_food.food_id
GROUP BY food.food_name;
