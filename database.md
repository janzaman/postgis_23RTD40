# Setting up database

-- Database: 23RTD40

-- DROP DATABASE IF EXISTS "23RTD40";

CREATE DATABASE "23RTD40"
    WITH
    OWNER = postgres
    ENCODING = 'UTF8'
    LC_COLLATE = 'Dutch_Belgium.1252'
    LC_CTYPE = 'Dutch_Belgium.1252'
    LOCALE_PROVIDER = 'libc'
    TABLESPACE = pg_default
    CONNECTION LIMIT = -1
    IS_TEMPLATE = False;
