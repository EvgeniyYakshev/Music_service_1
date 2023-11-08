-- Создание таблицы "Жанры"
CREATE TABLE IF NOT exists Genres (
    genre_id SERIAL PRIMARY KEY,
    title VARCHAR(60) NOT null UNIQUE
);

--Создание таблицы "Исполнители"
CREATE TABLE IF NOT exists Performers (
    performer_id SERIAL PRIMARY KEY,
    name_alias VARCHAR(60) NOT null
);

--Создание таблицы "Жанр-Исполнитель"
-- многие ко многим
CREATE TABLE IF NOT exists Genres_performers (
    g_id integer references Genres(genre_id),
    p_id integer references Performers(performer_id),
    constraint pg primary key (g_id, p_id)
);

--Создание таблицы "Альбомы"
CREATE TABLE IF NOT exists Albums (
    album_id SERIAL PRIMARY KEY,
    title VARCHAR(60) NOT null,
    year_of_release date NOT null,
    constraint year_rel CHECK (year_of_release > 2001)
);

--Создание таблицы "Альбом-Исполнитель"
-- многие ко многим
CREATE TABLE IF NOT exists albums_performers (
    a_id integer references Albums(album_id),
    per_id integer references Performers(performer_id),
    constraint aper primary key (a_id, per_id)
);

--Создание таблицы "Музыкальные треки"
-- один к одному
CREATE TABLE IF NOT exists Music_tracks (
    track_id serial primary key,
    title VARCHAR(60) NOT null,
    duration integer NOT null UNIQUE,
    alb_id integer references Albums(album_id)
);

--Создание таблицы "Сборник"
CREATE TABLE IF NOT exists Colection (
    colection_id SERIAL PRIMARY KEY,
    title VARCHAR(60) NOT null,
    year_of_release date NOT null,
    constraint year_reles CHECK (year_of_release > 2000)
);

--Создание таблицы "Сборник-Трек"
-- многие ко многим
CREATE TABLE IF NOT exists colections_tracks (
    id SERIAL PRIMARY KEY,
    c_id integer not null references Colection(colection_id),
    t_id integer not null references Music_tracks(track_id)
);

