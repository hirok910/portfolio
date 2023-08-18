# portfolio
授業の一環で作成したSNSサイト。
同じ学科の友人五名とグループで制作。

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+09:00";

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

CREATE DATABASE IF NOT EXISTS `welp` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
USE `welp`;

DROP TABLE IF EXISTS `favorites`;
CREATE TABLE `favorites` (
`id` int(11) NOT NULL,
`user_id` int(11) NOT NULL,
`post_id` int(11) NOT NULL,
`created_at` datetime NOT NULL DEFAULT current_timestamp()
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

DROP TABLE IF EXISTS `follows`;
CREATE TABLE `follows` (
`id` int(11) NOT NULL,
`from_id` int(11) NOT NULL,
`to_id` int(11) NOT NULL,
`created_at` datetime NOT NULL DEFAULT current_timestamp()
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

DROP TABLE IF EXISTS `images`;
CREATE TABLE `images` (
`id` int(11) NOT NULL,
`image_type` varchar(64) NOT NULL,
`image_content` mediumblob NOT NULL,
`image_size` int(11) NOT NULL,
`created_at` datetime NOT NULL DEFAULT current_timestamp()
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

DROP TABLE IF EXISTS `posts`;
CREATE TABLE `posts` (
`id` int(11) NOT NULL,
`user_id` int(11) NOT NULL,
`from_post_id` int(11) DEFAULT NULL,
`content` text NOT NULL,
`created_at` datetime NOT NULL DEFAULT current_timestamp()
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

DROP TABLE IF EXISTS `sessions`;
CREATE TABLE `sessions` (
`id` int(11) NOT NULL,
`user_id` int(11) NOT NULL,
`token` varchar(255) NOT NULL,
`created_at` datetime NOT NULL DEFAULT current_timestamp()
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

DROP TABLE IF EXISTS `users`;
CREATE TABLE `users` (
`id` int(11) NOT NULL,
`name` varchar(255) NOT NULL,
`email` varchar(255) NOT NULL,
`password` varchar(255) NOT NULL,
`picture_id` int(11) DEFAULT NULL,
`is_admin` tinyint(1) NOT NULL DEFAULT 0,
`created_at` datetime NOT NULL DEFAULT current_timestamp(),
`updated_at` datetime NOT NULL DEFAULT current_timestamp()
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;


ALTER TABLE `favorites`
ADD PRIMARY KEY (`id`);

ALTER TABLE `follows`
ADD PRIMARY KEY (`id`);

ALTER TABLE `images`
ADD PRIMARY KEY (`id`);

ALTER TABLE `posts`
ADD PRIMARY KEY (`id`);

ALTER TABLE `sessions`
ADD PRIMARY KEY (`id`);

ALTER TABLE `users`
ADD PRIMARY KEY (`id`),
ADD UNIQUE KEY `email` (`email`);


ALTER TABLE `favorites`
MODIFY `id` int(11) NOT NULL AUTO_INCREMENT;

ALTER TABLE `follows`
MODIFY `id` int(11) NOT NULL AUTO_INCREMENT;

ALTER TABLE `images`
MODIFY `id` int(11) NOT NULL AUTO_INCREMENT;

ALTER TABLE `posts`
MODIFY `id` int(11) NOT NULL AUTO_INCREMENT;

ALTER TABLE `sessions`
MODIFY `id` int(11) NOT NULL AUTO_INCREMENT;

ALTER TABLE `users`
MODIFY `id` int(11) NOT NULL AUTO_INCREMENT;
COMMIT;