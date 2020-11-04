# ProyectoBD1

CREATE TABLE bodega (
    id_bodega   INTEGER NOT NULL,
    nombre      VARCHAR2(100),
    direccion   VARCHAR2(100),
    tel_1       VARCHAR2(10),
    tel_2       VARCHAR2(10),
    correo      VARCHAR2(20),
    encargado   VARCHAR2(100)
);

ALTER TABLE bodega ADD CONSTRAINT bodega_pk PRIMARY KEY ( id_bodega );

CREATE TABLE caja (
    id_caja                      INTEGER NOT NULL,
    cantidad                     VARCHAR2(100),
    monto_unitario               NUMBER(17, 2),
    descuento                    NUMBER(17, 2),
    monto_total                  NUMBER(17, 2),
    cancelado                    NUMBER(17, 2),
    fecha                        DATE,
    nit                          VARCHAR2(10),
    estado_caja                  VARCHAR2(100),
    clinica_id_clinica           INTEGER NOT NULL,
    labo_id_labo                 INTEGER NOT NULL,
    cuent_a_pag_id_cuent_a_pag   INTEGER NOT NULL
);

ALTER TABLE caja ADD CONSTRAINT caja_pk PRIMARY KEY ( id_caja );

CREATE TABLE cita (
    id_cita                INTEGER NOT NULL,
    fecha                  DATE,
    hora                   DATE,
    traslado               VARCHAR2(100),
    clinica_id_clinica     INTEGER NOT NULL,
    labo_id_labo           INTEGER NOT NULL,
    servicio_id_servicio   INTEGER NOT NULL,
    cliente_id_cliente     INTEGER NOT NULL
);

ALTER TABLE cita ADD CONSTRAINT cita_pk PRIMARY KEY ( id_cita );

CREATE TABLE cliente (
    id_cliente   INTEGER NOT NULL,
    nombre       VARCHAR2(100),
    apellido     VARCHAR2(100),
    direccion    VARCHAR2(100),
    correo       VARCHAR2(20),
    nit          VARCHAR2(20)
);

ALTER TABLE cliente ADD CONSTRAINT cliente_pk PRIMARY KEY ( id_cliente );

CREATE TABLE clinica (
    id_clinica     INTEGER NOT NULL,
    nombre         VARCHAR2(100),
    tel_1          VARCHAR2(20),
    tel_2          VARCHAR2(10),
    correo         VARCHAR2(20),
    encargado      VARCHAR2(100),
    sede_id_sede   INTEGER NOT NULL
);

ALTER TABLE clinica ADD CONSTRAINT clinica_pk PRIMARY KEY ( id_clinica );

CREATE TABLE cobro (
    id_cobro          INTEGER NOT NULL,
    no_factura        VARCHAR2(10),
    monto_total       NUMBER(17, 2),
    monto_realizado   NUMBER(17, 2),
    forma_pago        VARCHAR2(100),
    caja_id_caja      INTEGER NOT NULL
);

ALTER TABLE cobro ADD CONSTRAINT cobro_pk PRIMARY KEY ( id_cobro );

CREATE TABLE cuad_caja (
    fecha           DATE,
    total_factura   NUMBER(17, 2),
    monto_caja      NUMBER(17, 2),
    id_cuad_caja    INTEGER NOT NULL,
    caja_id_caja    INTEGER NOT NULL
);

CREATE UNIQUE INDEX cuad_caja__idx ON
    cuad_caja (
        caja_id_caja
    ASC );

ALTER TABLE cuad_caja ADD CONSTRAINT cuad_caja_pk PRIMARY KEY ( id_cuad_caja );

CREATE TABLE cuent_a_pag (
    id_cuent_a_pag           INTEGER NOT NULL,
    no_factura               VARCHAR2(10),
    monto                    NUMBER(17, 2),
    monto_adeudado           NUMBER(17, 2),
    estado_cuenta            VARCHAR2(10),
    proveedor_id_proveedor   INTEGER NOT NULL
);

ALTER TABLE cuent_a_pag ADD CONSTRAINT cuent_a_pag_pk PRIMARY KEY ( id_cuent_a_pag );

CREATE TABLE empleado (
    id_empleado                    INTEGER NOT NULL,
    cod_empleado                   VARCHAR2(10),
    nombre                         VARCHAR2(100),
    apellido                       VARCHAR2(100),
    direccion                      VARCHAR2(100),
    tel_casa                       VARCHAR2(10),
    celular                        VARCHAR2(10),
    genero                         VARCHAR2(1),
    correo                         VARCHAR2(20),
    rol                            VARCHAR2(100),
    especialidad_id_especialidad   INTEGER NOT NULL,
    sede_id_sede                   INTEGER NOT NULL
);

ALTER TABLE empleado ADD CONSTRAINT empleado_pk PRIMARY KEY ( id_empleado );

CREATE TABLE especialidad (
    id_especialidad   INTEGER NOT NULL,
    descripcion       VARCHAR2(100)
);

ALTER TABLE especialidad ADD CONSTRAINT especialidad_pk PRIMARY KEY ( id_especialidad );

CREATE TABLE exped (
    id_expediente              INTEGER NOT NULL,
    edad                       VARCHAR2(4),
    peso                       VARCHAR2(5),
    tamaño                     VARCHAR2(10),
    tipo_sangre                VARCHAR2(5),
    genero                     VARCHAR2(1),
    alergico                   VARCHAR2(20),
    otra_enfermedad            VARCHAR2(50),
    cliente_id_cliente         INTEGER NOT NULL,
    sig_vital_id_signo_vital   INTEGER NOT NULL,
    clinica_id_clinica         INTEGER NOT NULL,
    empleado_id_empleado       INTEGER NOT NULL
);

CREATE UNIQUE INDEX exped__idx ON
    exped (
        cliente_id_cliente
    ASC );

ALTER TABLE exped ADD CONSTRAINT exped_pk PRIMARY KEY ( id_expediente );

CREATE TABLE factura (
    id_factura     INTEGER NOT NULL,
    no_factura     VARCHAR2(10),
    nombre         VARCHAR2(100),
    apellido       VARCHAR2(100),
    direccion      VARCHAR2(100),
    nit            VARCHAR2(10),
    fecha          DATE,
    cantidad       NUMBER(17, 2),
    descuento      NUMBER(17, 2),
    total          NUMBER(17, 2),
    caja_id_caja   INTEGER NOT NULL
);

ALTER TABLE factura ADD CONSTRAINT factura_pk PRIMARY KEY ( id_factura );

CREATE TABLE farmacia (
    id_farmacia        INTEGER NOT NULL,
    nombre             VARCHAR2(100),
    direccion          VARCHAR2(100),
    tel_1              VARCHAR2(10),
    tel_2              VARCHAR2(10),
    correo             VARCHAR2(20),
    encargado          VARCHAR2(100),
    bodega_id_bodega   INTEGER NOT NULL,
    sede_id_sede       INTEGER NOT NULL
);

ALTER TABLE farmacia ADD CONSTRAINT farmacia_pk PRIMARY KEY ( id_farmacia );

CREATE TABLE ingr_insumo (
    id_ingr_insumo           INTEGER NOT NULL,
    cantidad                 VARCHAR2(100),
    precio_compra            NUMBER(17, 2),
    no_factura               VARCHAR2(100),
    fecha_ingreso            DATE,
    bodega_id_bodega         INTEGER NOT NULL,
    proveedor_id_proveedor   INTEGER NOT NULL
);

ALTER TABLE ingr_insumo ADD CONSTRAINT ingr_insumo_pk PRIMARY KEY ( id_ingr_insumo );

CREATE TABLE insumo (
    id_insumo          INTEGER NOT NULL,
    descripcion        VARCHAR2(100),
    cantidad           VARCHAR2(100),
    fecha_caducidad    DATE,
    cod_barras         VARCHAR2(100),
    precio_venta       NUMBER(17, 2),
    stock_min          VARCHAR2(10),
    stock_max          VARCHAR2(10),
    bodega_id_bodega   INTEGER NOT NULL
);

ALTER TABLE insumo ADD CONSTRAINT insumo_pk PRIMARY KEY ( id_insumo );

CREATE TABLE labo (
    id_labo        INTEGER NOT NULL,
    nombre         VARCHAR2(100),
    direccion      VARCHAR2(100),
    encargado      VARCHAR2(100),
    tel_1          VARCHAR2(10),
    tel_2          VARCHAR2(10),
    correo         VARCHAR2(20),
    sede_id_sede   INTEGER NOT NULL
);

ALTER TABLE labo ADD CONSTRAINT labo_pk PRIMARY KEY ( id_labo );

CREATE TABLE proveedor (
    id_proveedor   INTEGER NOT NULL,
    tel_1          VARCHAR2(10),
    tel_2          VARCHAR2(10),
    nit            VARCHAR2(10),
    correo         VARCHAR2(20),
    nombre         VARCHAR2(100),
    direccion      VARCHAR2(100),
    contacto       VARCHAR2(100)
);

ALTER TABLE proveedor ADD CONSTRAINT proveedor_pk PRIMARY KEY ( id_proveedor );

CREATE TABLE sede (
    id_sede     INTEGER NOT NULL,
    nombre      VARCHAR2(100),
    direccion   VARCHAR2(100),
    tel_1       VARCHAR2(10),
    tel_2       VARCHAR2(10),
    correo      VARCHAR2(100),
    encargado   VARCHAR2(100)
);

ALTER TABLE sede ADD CONSTRAINT sede_pk PRIMARY KEY ( id_sede );

CREATE TABLE servicio (
    id_servicio   INTEGER NOT NULL,
    comentarios   VARCHAR2(100)
);

ALTER TABLE servicio ADD CONSTRAINT servicio_pk PRIMARY KEY ( id_servicio );

CREATE TABLE sig_vital (
    fecha                     DATE,
    id_signo_vital            INTEGER NOT NULL,
    presion_arterial          VARCHAR2(100),
    frecuencia_cardiaca       VARCHAR2(100),
    frecuencia_respiratoria   VARCHAR2(100),
    cliente_id_cliente        INTEGER NOT NULL
);

ALTER TABLE sig_vital ADD CONSTRAINT sig_vital_pk PRIMARY KEY ( id_signo_vital );

ALTER TABLE caja
    ADD CONSTRAINT caja_clinica_fk FOREIGN KEY ( clinica_id_clinica )
        REFERENCES clinica ( id_clinica );

ALTER TABLE caja
    ADD CONSTRAINT caja_cuent_a_pag_fk FOREIGN KEY ( cuent_a_pag_id_cuent_a_pag )
        REFERENCES cuent_a_pag ( id_cuent_a_pag );

ALTER TABLE caja
    ADD CONSTRAINT caja_labo_fk FOREIGN KEY ( labo_id_labo )
        REFERENCES labo ( id_labo );

ALTER TABLE cita
    ADD CONSTRAINT cita_cliente_fk FOREIGN KEY ( cliente_id_cliente )
        REFERENCES cliente ( id_cliente );

ALTER TABLE cita
    ADD CONSTRAINT cita_clinica_fk FOREIGN KEY ( clinica_id_clinica )
        REFERENCES clinica ( id_clinica );

ALTER TABLE cita
    ADD CONSTRAINT cita_labo_fk FOREIGN KEY ( labo_id_labo )
        REFERENCES labo ( id_labo );

ALTER TABLE cita
    ADD CONSTRAINT cita_servicio_fk FOREIGN KEY ( servicio_id_servicio )
        REFERENCES servicio ( id_servicio );

ALTER TABLE clinica
    ADD CONSTRAINT clinica_sede_fk FOREIGN KEY ( sede_id_sede )
        REFERENCES sede ( id_sede );

ALTER TABLE cobro
    ADD CONSTRAINT cobro_caja_fk FOREIGN KEY ( caja_id_caja )
        REFERENCES caja ( id_caja );

ALTER TABLE cuad_caja
    ADD CONSTRAINT cuad_caja_caja_fk FOREIGN KEY ( caja_id_caja )
        REFERENCES caja ( id_caja );

ALTER TABLE cuent_a_pag
    ADD CONSTRAINT cuent_a_pag_proveedor_fk FOREIGN KEY ( proveedor_id_proveedor )
        REFERENCES proveedor ( id_proveedor );

ALTER TABLE empleado
    ADD CONSTRAINT empleado_especialidad_fk FOREIGN KEY ( especialidad_id_especialidad )
        REFERENCES especialidad ( id_especialidad );

ALTER TABLE empleado
    ADD CONSTRAINT empleado_sede_fk FOREIGN KEY ( sede_id_sede )
        REFERENCES sede ( id_sede );

ALTER TABLE exped
    ADD CONSTRAINT exped_cliente_fk FOREIGN KEY ( cliente_id_cliente )
        REFERENCES cliente ( id_cliente );

ALTER TABLE exped
    ADD CONSTRAINT exped_clinica_fk FOREIGN KEY ( clinica_id_clinica )
        REFERENCES clinica ( id_clinica );

ALTER TABLE exped
    ADD CONSTRAINT exped_empleado_fk FOREIGN KEY ( empleado_id_empleado )
        REFERENCES empleado ( id_empleado );

ALTER TABLE exped
    ADD CONSTRAINT exped_sig_vital_fk FOREIGN KEY ( sig_vital_id_signo_vital )
        REFERENCES sig_vital ( id_signo_vital );

ALTER TABLE factura
    ADD CONSTRAINT factura_caja_fk FOREIGN KEY ( caja_id_caja )
        REFERENCES caja ( id_caja );

ALTER TABLE farmacia
    ADD CONSTRAINT farmacia_bodega_fk FOREIGN KEY ( bodega_id_bodega )
        REFERENCES bodega ( id_bodega );

ALTER TABLE farmacia
    ADD CONSTRAINT farmacia_sede_fk FOREIGN KEY ( sede_id_sede )
        REFERENCES sede ( id_sede );

ALTER TABLE ingr_insumo
    ADD CONSTRAINT ingr_insumo_bodega_fk FOREIGN KEY ( bodega_id_bodega )
        REFERENCES bodega ( id_bodega );

ALTER TABLE ingr_insumo
    ADD CONSTRAINT ingr_insumo_proveedor_fk FOREIGN KEY ( proveedor_id_proveedor )
        REFERENCES proveedor ( id_proveedor );

ALTER TABLE insumo
    ADD CONSTRAINT insumo_bodega_fk FOREIGN KEY ( bodega_id_bodega )
        REFERENCES bodega ( id_bodega );

ALTER TABLE labo
    ADD CONSTRAINT labo_sede_fk FOREIGN KEY ( sede_id_sede )
        REFERENCES sede ( id_sede );

ALTER TABLE sig_vital
    ADD CONSTRAINT sig_vital_cliente_fk FOREIGN KEY ( cliente_id_cliente )
        REFERENCES cliente ( id_cliente );

ALTER TABLE caja
    ADD CONSTRAINT caja_clinica_fk FOREIGN KEY ( clinica_id_clinica )
        REFERENCES clinica ( id_clinica );

ALTER TABLE caja
    ADD CONSTRAINT caja_cuent_a_pag_fk FOREIGN KEY ( cuent_a_pag_id_cuent_a_pag )
        REFERENCES cuent_a_pag ( id_cuent_a_pag );

ALTER TABLE caja
    ADD CONSTRAINT caja_labo_fk FOREIGN KEY ( labo_id_labo )
        REFERENCES labo ( id_labo );

ALTER TABLE cita
    ADD CONSTRAINT cita_cliente_fk FOREIGN KEY ( cliente_id_cliente )
        REFERENCES cliente ( id_cliente );

ALTER TABLE cita
    ADD CONSTRAINT cita_clinica_fk FOREIGN KEY ( clinica_id_clinica )
        REFERENCES clinica ( id_clinica );

ALTER TABLE cita
    ADD CONSTRAINT cita_labo_fk FOREIGN KEY ( labo_id_labo )
        REFERENCES labo ( id_labo );

ALTER TABLE cita
    ADD CONSTRAINT cita_servicio_fk FOREIGN KEY ( servicio_id_servicio )
        REFERENCES servicio ( id_servicio );

ALTER TABLE clinica
    ADD CONSTRAINT clinica_sede_fk FOREIGN KEY ( sede_id_sede )
        REFERENCES sede ( id_sede );

ALTER TABLE cobro
    ADD CONSTRAINT cobro_caja_fk FOREIGN KEY ( caja_id_caja )
        REFERENCES caja ( id_caja );

ALTER TABLE cuad_caja
    ADD CONSTRAINT cuad_caja_caja_fk FOREIGN KEY ( caja_id_caja )
        REFERENCES caja ( id_caja );

ALTER TABLE cuent_a_pag
    ADD CONSTRAINT cuent_a_pag_proveedor_fk FOREIGN KEY ( proveedor_id_proveedor )
        REFERENCES proveedor ( id_proveedor );

ALTER TABLE empleado
    ADD CONSTRAINT empleado_especialidad_fk FOREIGN KEY ( especialidad_id_especialidad )
        REFERENCES especialidad ( id_especialidad );

ALTER TABLE empleado
    ADD CONSTRAINT empleado_sede_fk FOREIGN KEY ( sede_id_sede )
        REFERENCES sede ( id_sede );

ALTER TABLE exped
    ADD CONSTRAINT exped_cliente_fk FOREIGN KEY ( cliente_id_cliente )
        REFERENCES cliente ( id_cliente );

ALTER TABLE exped
    ADD CONSTRAINT exped_clinica_fk FOREIGN KEY ( clinica_id_clinica )
        REFERENCES clinica ( id_clinica );

ALTER TABLE exped
    ADD CONSTRAINT exped_empleado_fk FOREIGN KEY ( empleado_id_empleado )
        REFERENCES empleado ( id_empleado );

ALTER TABLE exped
    ADD CONSTRAINT exped_sig_vital_fk FOREIGN KEY ( sig_vital_id_signo_vital )
        REFERENCES sig_vital ( id_signo_vital );

ALTER TABLE factura
    ADD CONSTRAINT factura_caja_fk FOREIGN KEY ( caja_id_caja )
        REFERENCES caja ( id_caja );

ALTER TABLE farmacia
    ADD CONSTRAINT farmacia_bodega_fk FOREIGN KEY ( bodega_id_bodega )
        REFERENCES bodega ( id_bodega );

ALTER TABLE farmacia
    ADD CONSTRAINT farmacia_sede_fk FOREIGN KEY ( sede_id_sede )
        REFERENCES sede ( id_sede );

ALTER TABLE ingr_insumo
    ADD CONSTRAINT ingr_insumo_bodega_fk FOREIGN KEY ( bodega_id_bodega )
        REFERENCES bodega ( id_bodega );

ALTER TABLE ingr_insumo
    ADD CONSTRAINT ingr_insumo_proveedor_fk FOREIGN KEY ( proveedor_id_proveedor )
        REFERENCES proveedor ( id_proveedor );

ALTER TABLE insumo
    ADD CONSTRAINT insumo_bodega_fk FOREIGN KEY ( bodega_id_bodega )
        REFERENCES bodega ( id_bodega );

ALTER TABLE labo
    ADD CONSTRAINT labo_sede_fk FOREIGN KEY ( sede_id_sede )
        REFERENCES sede ( id_sede );

ALTER TABLE sig_vital
    ADD CONSTRAINT sig_vital_cliente_fk FOREIGN KEY ( cliente_id_cliente )
        REFERENCES cliente ( id_cliente );
