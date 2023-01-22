1) Crear Base de datos
    use ecommerce;
2) Crear colecciones
    db.createCollection('productos');
    db.createCollection('mensajes')

3) Insertar los productos: 

db.productos.insertMany([
    {
        "timestamp": ISODate(),
        "title": "Cargador",
        "price": 105,
        "description":"Cargador Celu",
        "code": "CS-1",
        "image": "imagen1.com",
        "stock": 420
    },
    {
        "timestamp": ISODate(),
        "title": "Auricular",
        "price": 320,
        "description":"Auriculares baratos",
        "code": "CS-2",
        "image": "imagen2.com",
        "stock": 221
    },
    {
        "timestamp": ISODate(),
        "title": "Cable HDMI",
        "price": 930,
        "description":"Cable de conexión HDMI",
        "code": "CS-3",
        "image": "imagen3.com",
        "stock": 200                    
    },
    {
        "timestamp": ISODate(),
        "title": "Parlantes",
        "price": 1140,
        "description":"Parlantes PC marca Next",
        "code": "CS-4",
        "image": "imagen4.com",
        "stock": 102                
    },
    {
        "timestamp": ISODate(),
        "title": "Teclado Gamer",
        "price": 2250,
        "description":"Teclado gamer económico",
        "code": "CS-5",
        "image": "imagen5.com",
        "stock": 40     
    },
    {
        "timestamp": ISODate(),
        "title": "Teclado Genius",
        "price": 3360,
        "description":"Teclado Marca Genius",
        "code": "CS-6",
        "image": "imagen6.com",
        "stock": 247
    },
    {
        "timestamp": ISODate(),
        "title": "Fuente de energía 100 wats",
        "price": 4470,
        "description":"Fuente de Energía para PC Gamer",
        "code": "CS-7",
        "image": "imagen7.com",
        "stock": 14
    },
    {
        "timestamp": ISODate(),
        "title": "Memoria RAM 1gb",
        "price": 5000,
        "description":"Tarjeta de memoria ram",
        "code": "CS-8",
        "image": "imagen8.com",
        "stock": 700
    },
    {
        "timestamp": ISODate(),
        "title": "Impresora",
        "price": 3450,
        "description":"Impresora marca HP",
        "code": "CS-9",
        "image": "imagen9.com",
        "stock": 900
    },
    {
        "timestamp": ISODate(),
        "title": "Kit Mouse + Teclado",
        "price": 2860,
        "description":"Kit de teclado y mouse marca Genius",
        "code": "CS-10",
        "image": "imagen10.com",
        "stock": 1000
    }
]);

4) Listar todos los productos:
    db.productos.find();

5) Contar la cantidad de documentos en productos
    db.productos.countDocuments()

5) CRUD sobre la colección de productos
    a) Agregar otro producto más a productos:
            db.productos.insertOne({
                "timestamp": ISODate(),
                "title": "Disco duro externo",
                "price": 3860,
                "description":"Disco duro externo de 64gb",
                "code": "CS-11",
                "image": "imagen11.com",
                "stock": 540
            });
    
    b) Realizar consulta por nombre de producto específico
        db.productos.find({code: "CS-11"}, {title: 1, _id:0}); // Devuelve un producto con nombre "CS-11"

        i) Listar los productos con precio menor a 1000 pesos
            db.productos.find({price: {$lt: 1000}});

        ii) Listar los productos con precio entre los 1000 a 3000 pesos
            db.productos.find({price: {$gt: 1000, $lt: 3000 });

        iii) Listar los productos con precio mayor a 3000 pesos.
            db.productos.find({price: {$gt: 3000}});
        
        iv) Realizar una consulta que traiga sólo el nombre del tercer producto más barato
            db.productos.find({},{title:1, _id:0}).sort({price:1}).skip(2).limit(1);

    c) Hacer una actualización sobre todos los productos, agregando el campo stock a todos ellos con un valor de 100
            db.productos.updateMany({}, {$inc: {stock: 100}});
    
    d) Cambiar el stock a cero de los productos con precios mayores a 4000 pesos.
            db.productos.updateMany({price: {$gt: 4000}}, {$set: {stock: 0}});

    e) Borrar los productos con precio menor a 1000 pesos
            db.productos.deleteMany({price: {$lt: 1000}});

6) Crear un usuario 'pepe' clave: 'asd456' que solo pueda leer la base de datos ecommerce. Verificar que pepe no pueda cambiar la información
            db.createUser({user: "pepe", pwd: "asd456", roles: [{role: "read", db: "ecommerce"}]});