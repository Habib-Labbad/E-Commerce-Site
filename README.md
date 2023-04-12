Please install Mondodb first.
1- create database using "use vue-db"
2- db.products.insertMany([{},{},{},,,]) ..please copy this data from the file fsv-front-end/src/fake-data.js one by one
3- db.users.insertOne({
    id: "12345",
    cartItems:[
        '123',
        '234',
        '456',
        ]
})
4- install the Mondodb driver in thr project "npm install mongodb"
5- run "npm run dev" in the back-end
6- run "npm serve in the front-end"

