#include <stdio.h>
#include <stdlib.h>
#include <string.h>


#define Maximo 50
typedef char string[Maximo];

typedef struct {
    string id_producto;
    string descripcion;
    float precioCompra;
    float precioVenta;
    string unidadMedida;
    float stock;
    string id_proveedor;
} producto;

producto tProductos[100];

typedef struct {
    string id_proveedor;
    string nombre;
    string calle;
    string colonia;
    string ciudad;
    string pais;
    string telefono;
    string mail;
} proveedor;

proveedor tProveedores[20];

typedef struct {
    int id_cliente;
    string nombre;
    string calle;
    string colonia;
    string ciudad;
    string pais;
    string telefono;
    string mail;
} cliente;

cliente tclientes[20];

typedef struct {
    int id_venta;
    string fecha;
    string id_producto;
    float cantidad;
    float importe;
    string id_cliente;
} venta;

venta tVentas[1000];

typedef struct {
    int id_compra;
    string fecha;
    string id_producto;
    float cantidad;
    float importe;
    string id_proveedor;
} compra;

compra tCompras[1000];

void inicializaProductos();
void listarProductos();
int buscarLugar();
void pedirDatosProductos();
void grabarDatosProductos(producto tProductos[], int llave, string idP, string des, string uM, float pC, float pV, float sT, string idPv);
int buscarProducto(producto tProductos[], string idP);
void desplegarProducto(producto tProductos[]);
void bajaDatosProducto(producto tProductos[], int llave);
void listo();


void inicializaClientes();
void listarClientes();
void bajaDatosClientes(cliente tClientes[], int llave);
void pedirDatosClientes();
void grabarDatosClientes(cliente tClientes[], int llave, int idC, string nombre, string calle, string colonia, string ciudad, string pais, string telefono, string mail);
int buscarClientes(cliente tClientes[], int idC);
void desplegarClientes(cliente tClientes[]);

void inicializaProveedores();
void listarProveedores();
void bajaDatosProveedor(proveedor tProveedores[], int llave);
void pedirDatosProveedor();
void grabarDatosProveedor(proveedor tProveedores[], int llave, string idPv, string nombre, string calle, string colonia, string ciudad, string pais, string telefono, string mail);
int buscarProveedor(proveedor tProveedores[], string idPv);
void desplegarProveedor(proveedor tProveedores[]);


void inicializaCompras();
void listarCompras();
void bajaDatosCompra(compra tCompras[], int llave);
void pedirDatosCompra();
void grabarDatosCompra(compra tCompras[], int llave, int idC, string fecha, string idP, float cantidad, float importe, string idPv);
int buscarCompra(compra tCompras[], int idC);
void desplegarCompra(compra tCompras[]);

void inicializaVentas();
void listarVentas();
void bajaDatosVentas(venta tVentas[], int llave);
void pedirDatosVenta();
void grabarDatosVenta(venta tVentas[], int llave, int idV, string fecha, string idP, float cantidad, float importe, string idC);
int buscarVentas(venta tVentas[],int idV);
void desplegarVenta(venta tVentas[]);
void menuPrincipal();
void menuOperaciones();

int op1, op2, op3, op4, op5, op6, i, bajaProducto, opModificar;
int llave;
string idP, idPv, des, uM;
float pC, pV, sT;

string fecha,nombre,calle,colonia,ciudad,pais,telefono,mail;
string idV;
int idC;

int main() {
    op1 = 0;
    while (op1 < 6) {
        system("cls");
        printf("\n\t\t\t\t Menu principal");
        menuPrincipal();
        printf("\n\t\tDame la opcion->");
        scanf("%i", &op1);
        fflush(stdin);
        switch (op1) {
            case 1:
                op2=0;
                while(op2<7){
                    system("cls");
                    printf("\n\t\t\t\t Menu de Productos");
                    menuOperaciones();
                    printf("\n\n\t\t Dame opcion->");
                    scanf("%i",&op2);
                    fflush(stdin);
                    switch(op2){
                        case 1:
                            system("cls");
                            printf("\n\t\t\t\t Probar si hay lugar y en que llave");
                            if(buscarLugar()==1){
                                printf("\n Si hay lugar y la llave es [%i]",llave);
                                pedirDatosProductos();
                                grabarDatosProductos(tProductos,llave,idP,des,uM,pC,pV,sT,idPv);
                                printf("\n\n Listo Producto dado de alta teclea Enter");
                                getchar();
                            }else{
                                printf("\n No hay Lugar y la lleve es [%i]",llave);
                                getchar();
                            }
                            break;
                        case 2:
                            system("cls");
                            printf("\n\t\t\t\t\t Baja de Productos");
                            printf("\n\n\n\t\t Dame clave del Producto A dar de baja->");
                            scanf("%s",idP);
                            fflush(stdin);
                            if (buscarProducto(tProductos,idP)<100){
                                desplegarProducto(tProductos);
                                printf("\n\n Lo das de Baja Si=1 No=0->");
                                scanf("%i",&bajaProducto);
                                fflush(stdin);
                                if(bajaProducto==1){
                                    bajaDatosProducto(tProductos,llave);
                                    printf("\n Listo teclea Enter");
                                    getchar();
                                }else{
                                printf("\n\t Ok no doy de baja teclea Enter");
                                getchar();
                                }
                            }else{
                                printf("\n es eproducto no existe teclea Enter->");
                                getchar();
                            }
                            break;
                        case 3:
                            system("cls");
                            printf("\n\t\t\t\t\t Modificación de Información");
                            printf("\n\n Dame Clave del Producto->");
                            scanf("%s",&idP);
                            fflush(stdin);
                            if (buscarProducto(tProductos,idP)<100){
                                desplegarProducto(tProductos);
                                printf("\n\t\t Dame la opcion que quieres Modificar->");
                                scanf("%i",&opModificar);
                                fflush(stdin);
                                switch(opModificar){
                                    case 1:
                                        printf("\n La clave no se puede modificar teclea enter");
                                        getchar();
                                        break;
                                    case 2:
                                        printf("\n Dame nueva descripcion->");
                                        scanf("%s",&tProductos[llave].descripcion);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 3:
                                        printf("\n dame nueva unidad de Medida->");
                                        scanf("%s",&tProductos[llave].unidadMedida);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 4:
                                        printf("\n Dame nuevo precio Compra->");
                                        scanf("%f",&tProductos[llave].precioCompra);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 5:
                                        printf("\n Dame nuevo precio Venta->");
                                        scanf("%f",&tProductos[llave].precioVenta);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 6:
                                        printf("\n Dame nuevo Stock->");
                                        scanf("%f",&tProductos[llave].stock);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 7:
                                        printf("\n Dame nueva Clave de Proveedor->");
                                        scanf("%f",&tProductos[llave].id_proveedor);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    default:
                                        printf("\n No se hacen Cambios teclea Enter->");
                                        getchar();
                                        break;
                                                    }

                           }else{
                              printf("\n\n\t\t Oye que pasa información no existe para ese producto teclea Enter");
                              getchar();
                                }
                            break;
                        case 4:
                            system("cls");
                            printf("\n\t\t\t\t\t Consulta datos de Productos");
                            printf("\n\n\n\t\t Dame clave a consultar->");
                            scanf("%s",&idP);
                            fflush(stdin);
                            if (buscarProducto(tProductos,idP)<100){
                               desplegarProducto(tProductos);
                               printf("\n\n\n\t\t\t\t Listo esta es tu informacion Teclea Enter");
                               getchar();
                        }   else{
                               printf("\n\t\t No hay Información para esa clave teclea Enter");
                               getchar();
                                }
                            break;
                        case 5:
                            system("cls");
                            printf("\n\t\t\t\t\tListado de productos");
                            listarProductos();
                            printf("\n He terminado de listar tus productos teclea cualquier tecla");
                            getchar();
                            break;
                        case 6:
                            system("cls");
                            printf("\n\t\t\t\tEstamos inicializando");
                            inicializaProductos();
                            printf("\n he terminado de inizializar teclea cualquier tecla");
                            getchar();
                            break;
                             }
                         }
                         break;
            case 2:
                op3 = 0;
                while (op3 < 7) {
                    system("cls");
                    printf("\n\t\t\t\t Menu de Clientes");
                    menuOperaciones();
                    printf("\n\n\t\tDame opcion->");
                    scanf("%i", &op3);
                    fflush(stdin);
                    switch (op3) {
                          case 1:
                            system("cls");
                            printf("\n\t\t\t\t Probar si hay lugar y en que llave");
                            if (buscarClientes(tclientes,idC) == 0) {
                              printf("\n Si hay lugar y la llave es [%i]", llave);
                              pedirDatosClientes();
                              void grabarDatosClientes(cliente tClientes[], int llave, int idC, string nombre, string calle, string colonia, string ciudad, string pais, string telefono, string mail);
                              printf("\n\n Listo cliente dado de alta teclea Enter");
                              getchar();
                            } else {
                              printf("\n No hay Lugar y la llave es [%i]", llave);
                              getchar();
                                   }
                            break;
                        case 2:
                            system("cls");
                            printf("\n\t\t\t\t\t Baja de cliente");
                            printf("\n\n\n\t\t Dame clave del cliente A dar de baja->");
                            scanf("%s", idC);
                            fflush(stdin);
                            if (buscarClientes(tclientes, idC) < 100) {
                                desplegarClientes(tclientes);
                                printf("\n\n Lo das de Baja Si=1 No=0->");
                                scanf("%i", &bajaDatosClientes);
                                fflush(stdin);
                                if (bajaDatosClientes == 1) {
                                    bajaDatosClientes(tclientes, llave);
                                    printf("\n Listo teclea Enter");
                                    getchar();
                                } else {
                                    printf("\n\t Ok no doy de baja teclea Enter");
                                    getchar();
                                }
                            } else {
                                printf("\n ese cliente no existe teclea Enter->");
                                getchar();
                            }
                            break;
                        case 3:
                            system("cls");
                            printf("\n\t\t\t\t\t Modificación de Información");
                            printf("\n\n Dame Clave del cliente>");
                            scanf("%s", &idC);
                            fflush(stdin);
                            if (buscarClientes(tclientes, idC) < 100) {
                                desplegarClientes(tclientes);
                                printf("\n\t\t Dame la opcion que quieres Modificar->");
                                scanf("%i", &opModificar);
                                fflush(stdin);
                                switch (opModificar) {
                                    case 1:
                                        printf("\n La clave no se puede modificar teclea enter");
                                        getchar();
                                        break;
                                    case 2:
                                        printf("\n Dame el nuevo mail->");
                                        scanf("%s", &tclientes[llave].mail);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 3:
                                        printf("\n dame nueva calle->");
                                        scanf("%s", &tclientes[llave].calle);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 4:
                                        printf("\n Dame nuevo colonia->");
                                        scanf("%f", &tclientes[llave].colonia);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 5:
                                        printf("\n Dame nueva ciudad->");
                                        scanf("%f", &tclientes[llave].ciudad);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 6:
                                        printf("\n Dame nueva calle->");
                                        scanf("%f", &tclientes[llave].calle);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 7:
                                        printf("\n Dame nueva Clave de Proveedor->");
                                        scanf("%f", &tclientes[llave].id_cliente);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    default:
                                        printf("\n No se hacen Cambios teclea Enter->");
                                        getchar();
                                        break;
                                }
                            } else {
                                printf("\n\n\t\t Oye que pasa información no existe para ese cliente teclea Enter");
                                getchar();
                            }
                            break;
                        case 4:
                            system("cls");
                            printf("\n\t\t\t\t\t Consulta datos de cliente");
                            printf("\n\n\n\t\t Dame clave a consultar->");
                            scanf("%s", &idC);
                            fflush(stdin);
                            if (buscarClientes(tclientes, idC) < 100) {
                                desplegarClientes(tclientes);
                                printf("\n\n\n\t\t\t\t Listo esta es tu informacion Teclea Enter");
                                getchar();
                            } else {
                                printf("\n\t\t No hay Información para esa clave teclea Enter");
                                getchar();
                            }
                            break;
                        case 5:
                            system("cls");
                            printf("\n\t\t\t\t\tListado de clientes");
                            listarClientes();
                            printf("\n He terminado de listar tus clientes teclea cualquier tecla");
                            getchar();
                            break;
                        case 6:
                            system("cls");
                            printf("\n\t\t\t\tEstamos inicializando");
                            inicializaClientes();
                            printf("\n he terminado de inizializar teclea cualquier tecla");
                            getchar();
                            break;
                    }
                }
                break;
            case 3:
                op4 = 0;
                while (op4<7) {
                    system("cls");
                    printf("\n\t\t\t\t Menu de Proveedores");
                    menuOperaciones();
                    printf("\n\n\t\t Dame opcion->");
                    scanf("%i", &op4);
                    fflush(stdin);
                    switch (op4) {
                        case 1:
                            system("cls");
                            printf("\n\t\t\t\t Probar si hay lugar y en que llave");
                            if (buscarProveedor(tProveedores,idPv) == 0) {
                                printf("\n Si hay lugar y la llave es [%i]", llave);
                                pedirDatosProveedor();
                                grabarDatosProveedor(tProveedores,llave,idPv,nombre,calle,colonia,ciudad,pais,telefono,mail);
                                printf("\n\n Listo Producto dado de alta teclea Enter");
                                getchar();
                            } else {
                                printf("\n No hay Lugar y la lleve es [%i]", llave);
                                getchar();
                            }
                            break;
                        case 2:
                            system("cls");
                            printf("\n\t\t\t\t\t Baja de proveedores");
                            printf("\n\n\n\t\t Dame clave del proveedor A dar de baja->");
                            scanf("%s", idPv);
                            fflush(stdin);
                            if (buscarProveedor(tProveedores, idPv) < 100) {
                                desplegarProveedor(tProveedores);
                                printf("\n\n Lo das de Baja Si=1 No=0->");
                                scanf("%i", &bajaDatosProveedor);
                                fflush(stdin);
                                if (bajaDatosProveedor == 1) {
                                    bajaDatosProveedor(tProveedores, llave);
                                    printf("\n Listo teclea Enter");
                                    getchar();
                                } else {
                                    printf("\n\t Ok no doy de baja teclea Enter");
                                    getchar();
                                }
                            } else {
                                printf("\n ese producto no existe teclea Enter->");
                                getchar();
                            }
                            break;
                        case 3:
                            system("cls");
                            printf("\n\t\t\t\t\t Modificación de Información");
                            printf("\n\n Dame Clave del proveedor->");
                            scanf("%s", &idPv);
                            fflush(stdin);
                            if (buscarProveedor(tProveedores, idPv) < 100) {
                                desplegarProveedor(tProveedores);
                                printf("\n\t\t Dame la opcion que quieres Modificar->");
                                scanf("%i", &opModificar);
                                fflush(stdin);
                                switch (opModificar) {
                                    case 1:
                                        printf("\n La clave no se puede modificar teclea enter");
                                        getchar();
                                        break;
                                    case 2:
                                        printf("\n Dame nueva calle->");
                                        scanf("%s", &tProveedores[llave].calle);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 3:
                                        printf("\n dame nueva ciudad->");
                                        scanf("%s", &tProveedores[llave].ciudad);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 4:
                                        printf("\n Dame nueva colonia->");
                                        scanf("%f", &tProveedores[llave].colonia);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 5:
                                        printf("\n Dame nueva id de proveedor->");
                                        scanf("%s", &tProveedores[llave].id_proveedor);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 6:
                                        printf("\n Dame nuevo mail->");
                                        scanf("%s", &tProveedores[llave].mail);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 7:
                                        printf("\n Dame nuevo nombre->");
                                        scanf("%s", &tProveedores[llave].nombre);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 8:
                                        printf("\n Dame nuevo pais->");
                                        scanf("%s", &tProveedores[llave].pais);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 9:
                                        printf("\n Dame nuevo telefono->");
                                        scanf("%s", &tProveedores[llave].telefono);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    default:
                                        printf("\n No se hacen Cambios teclea Enter->");
                                        getchar();
                                        break;
                                }
                            }else {
                                printf("\n\n\t\t Oye que pasa información no existe para ese proveedor teclea Enter");
                                getchar();
                            }
                            break;
                        case 4:
                            system("cls");
                            printf("\n\t\t\t\t\t Consulta datos de proveedor");
                            printf("\n\n\n\t\t Dame clave a consultar->");
                            scanf("%s", &idPv);
                            fflush(stdin);
                            if (buscarProveedor(tProveedores, idPv) < 100) {
                                desplegarProveedor(tProveedores);
                                printf("\n\n\n\t\t\t\t Listo esta es tu informacion Teclea Enter");
                                getchar();
                           }else {
                                printf("\n\t\t No hay Información para esa clave teclea Enter");
                                getchar();
                            }
                            break;
                        case 5:
                            system("cls");
                            printf("\n\t\t\t\t\tListado de proveedores");
                            listarProveedores();
                            printf("\n He terminado de listar tus proveedores teclea cualquier tecla");
                            getchar();
                            break;
                        case 6:
                            system("cls");
                            printf("\n\t\t\t\tEstamos inicializando");
                            inicializaProveedores();
                            printf("\n he terminado de inizializar teclea cualquier tecla");
                            getchar();
                            break;
                                }
                             }
                break;
            case 4:
                op5 = 0;
                while (op5 <7) {
                    system("cls");
                    printf("\n\t\t\t\t Menu de Ventas");
                    menuOperaciones();
                    printf("\n\n\t\t Dame opcion->");
                    scanf("%i", &op5);
                    fflush(stdin);
                    switch (op5) {
                        case 1:
                            system("cls");
                            printf("\n\t\t\t\t Probar si hay lugar y en que llave");
                           if  (buscarVentas(tVentas, idV) ==0) {
                                printf("\n Si hay lugar y la llave es [%i]", llave);
                                pedirDatosVenta();
                                void grabarDatosVenta(venta tVentas[], int llave, int idV, string fecha, string idP, float cantidad, float importe, string idC);
                                printf("\n\n Listo venta dada de alta teclea Enter");
                                getchar();
                            } else {
                                printf("\n No hay Lugar y la lleve es [%i]", llave);
                                getchar();
                            }
                            break;
                        case 2:
                            system("cls");
                            printf("\n\t\t\t\t\t Baja de venta");
                            printf("\n\n\n\t\t Dame clave de la venta A dar de baja->");
                            scanf("%s", idV);
                            fflush(stdin);
                            if (buscarVentas(tVentas, idV) < 1000) {
                                desplegarVenta(tVentas);
                                printf("\n\n Lo das de Baja Si=1 No=0->");
                                scanf("%i", &bajaDatosVentas);
                                fflush(stdin);
                                if (bajaDatosVentas == 1) {
                                    bajaDatosVentas(tVentas, llave);
                                    printf("\n Listo teclea Enter");
                                    getchar();
                                } else {
                                    printf("\n\t Ok no doy de baja teclea Enter");
                                    getchar();
                                }
                            } else {
                                printf("\n es eproducto no existe teclea Enter->");
                                getchar();
                            }
                            break;
                        case 3:
                            system("cls");
                            printf("\n\t\t\t\t\t Modificación de Información");
                            printf("\n\n Dame Clave de ventas->");
                            scanf("%s", &idV);
                            fflush(stdin);
                            if (buscarVentas(tVentas, idV) < 100) {
                                desplegarVenta(tVentas);
                                printf("\n\t\t Dame la opcion que quieres Modificar->");
                                scanf("%i", &opModificar);
                                fflush(stdin);
                                switch (opModificar) {
                                    case 1:
                                        printf("\n La clave no se puede modificar teclea enter");
                                        getchar();
                                        break;
                                    case 2:
                                        printf("\n Dame nueva cantidad->");
                                        scanf("%s", &tVentas[llave].cantidad);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 3:
                                        printf("\n dame nueva fecha->");
                                        scanf("%s", &tVentas[llave].fecha);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 4:
                                        printf("\n Dame nuevo id del cliente->");
                                        scanf("%f", &tVentas[llave].id_cliente);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 5:
                                        printf("\n Dame nuevo id del producto->");
                                        scanf("%f", &tVentas[llave].id_producto);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 6:
                                        printf("\n Dame nuevo id de venta->");
                                        scanf("%f", &tVentas[llave].id_venta);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 7:
                                        printf("\n Dame nueva importe->");
                                        scanf("%f", &tVentas[llave].importe);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    default:
                                        printf("\n No se hacen Cambios teclea Enter->");
                                        getchar();
                                        break;
                                }
                            } else {
                                printf("\n\n\t\t Oye que pasa información no existe para ese producto teclea Enter");
                                getchar();
                            }
                            break;
                        case 4:
                            system("cls");
                            printf("\n\t\t\t\t\t Consulta datos de ventas");
                            printf("\n\n\n\t\t Dame clave a consultar->");
                            scanf("%s", &idV);
                            fflush(stdin);
                            if (buscarVentas(tVentas,idV) < 1000) {
                                desplegarVenta(tVentas);
                                printf("\n\n\n\t\t\t\t Listo esta es tu informacion Teclea Enter");
                                getchar();
                            } else {
                                printf("\n\t\t No hay Información para esa clave teclea Enter");
                                getchar();
                            }
                            break;
                        case 5:
                            system("cls");
                            printf("\n\t\t\t\t\tListado de ventas");
                            listarVentas();
                            printf("\n He terminado de listar tus productos teclea cualquier tecla");
                            getchar();
                            break;
                        case 6:
                            system("cls");
                            printf("\n\t\t\t\tEstamos inicializando");
                            inicializaVentas();
                            printf("\n he terminado de inizializar teclea cualquier tecla");
                            getchar();
                            break;
                    }
                }
                break;
            case 5:
                op6 = 0;
                while (op6 < 7) {
                    system("cls");
                    printf("\n\t\t\t\t Menu de Compras");
                    menuOperaciones();
                    scanf("%i", &op6);
                    fflush(stdin);
                    switch (op6) {
                        case 1:
                            system("cls");
                            printf("\n\t\t\t\t Probar si hay lugar y en que llave");
                            if (buscarCompra(tCompras,idC) == 0) {
                                printf("\n Si hay lugar y la llave es [%i]", llave);
                                pedirDatosCompra();
                                void grabarDatosCompra(compra tCompras[], int llave, int idC, string fecha, string idP, float cantidad, float importe, string idPv);
                                printf("\n\n Listo compra dado de alta teclea Enter");
                                getchar();
                            } else {
                                printf("\n No hay Lugar y la lleve es [%i]", llave);
                                getchar();
                            }
                            break;
                        case 2:
                            system("cls");
                            printf("\n\t\t\t\t\t Baja de compras");
                            printf("\n\n\n\t\t Dame clave de la compra A dar de baja->");
                            scanf("%s", idC);
                            fflush(stdin);
                            if (buscarCompra(tCompras,idC) < 100) {
                                desplegarCompra(tCompras);
                                printf("\n\n Lo das de Baja Si=1 No=0->");
                                scanf("%i", &bajaDatosCompra);
                                fflush(stdin);
                                if (bajaDatosCompra == 1) {
                                    bajaDatosCompra(tCompras, llave);
                                    printf("\n Listo teclea Enter");
                                    getchar();
                                } else {
                                    printf("\n\t Ok no doy de baja teclea Enter");
                                    getchar();
                                }
                            } else {
                                printf("\n ese producto no existe teclea Enter->");
                                getchar();
                            }
                            break;
                        case 3:
                            system("cls");
                            printf("\n\t\t\t\t\t Modificación de Información");
                            printf("\n\n Dame Clave de compras->");
                            scanf("%s", &idC);
                            fflush(stdin);
                            if (buscarCompra(tCompras, idP) < 100) {
                                desplegarCompra(tProductos);
                                printf("\n\t\t Dame la opcion que quieres Modificar->");
                                scanf("%i", &opModificar);
                                fflush(stdin);
                                switch (opModificar) {
                                    case 1:
                                        printf("\n La clave no se puede modificar teclea enter");
                                        getchar();
                                        break;
                                    case 2:
                                        printf("\n Dame nueva id compra->");
                                        scanf("%s", &tCompras[llave].id_compra);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 3:
                                        printf("\n dame nueva fecha->");
                                        scanf("%s", &tCompras[llave].fecha);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 4:
                                        printf("\n Dame nuevo id de compra->");
                                        scanf("%f", &tCompras[llave].id_compra);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 5:
                                        printf("\n Dame nuevo id del producto->");
                                        scanf("%f", &tCompras[llave].id_producto);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 6:
                                        printf("\n Dame nuevo id de la venta->");
                                        scanf("%f", &tCompras[llave].id_proveedor);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    case 7:
                                        printf("\n Dame nuevo importe->");
                                        scanf("%f", &tCompras[llave].importe);
                                        fflush(stdin);
                                        listo();
                                        break;
                                    default:
                                        printf("\n No se hacen Cambios teclea Enter->");
                                        getchar();
                                        break;
                                }
                            } else {
                                printf("\n\n\t\t Oye que pasa información no existe para ese producto teclea Enter");
                                getchar();
                            }
                            break;
                        case 4:
                            system("cls");
                            printf("\n\t\t\t\t\t Consulta datos de compras");
                            printf("\n\n\n\t\t Dame clave a consultar->");
                            scanf("%s", &idC);
                            fflush(stdin);
                            if (buscarCompra(tCompras, idC) < 100) {
                                desplegarCompra(tCompras);
                                printf("\n\n\n\t\t\t\t Listo esta es tu informacion Teclea Enter");
                                getchar();
                            } else {
                                printf("\n\t\t No hay Información para esa clave teclea Enter");
                                getchar();
                            }
                            break;
                        case 5:
                            system("cls");
                            printf("\n\t\t\t\t\tListado de compras");
                            listarCompras();
                            printf("\n He terminado de listar tus productos teclea cualquier tecla");
                            getchar();
                            break;
                        case 6:
                            system("cls");
                            printf("\n\t\t\t\tEstamos inicializando");
                            inicializaCompras();
                            printf("\n he terminado de inizializar teclea cualquier tecla");
                            getchar();
                            break;
                    }
                }
                break;
        }
    }
    return 0;
        }

void menuPrincipal() {
    printf("\n\n\n\t\t\t\t1.- Mantenimiento a Productos");
    printf("\n\t\t\t\t2.- Mantenimiento a Clientes");
    printf("\n\t\t\t\t3.- Mantenimiento a Proveedores");
    printf("\n\t\t\t\t4.- Mantenimiento a Ventas");
    printf("\n\t\t\t\t5.- Mantenimiento a Compras");
    printf("\n\t\t\t\t6.- Salir");
}

void menuOperaciones() {
    printf("\n\t\t\t\t1.- Insercion");
    printf("\n\t\t\t\t2.- Borrado");
    printf("\n\t\t\t\t3.- Modificacion");
    printf("\n\t\t\t\t4.- Consulta");
    printf("\n\t\t\t\t5.- Listado");
    printf("\n\t\t\t\t6.- Inicializa");
    printf("\n\t\t\t\t7.- Regresar");
}

void inicializaProductos(){
for(i=0; i<100; i++){
    strcpy(tProductos[i].id_producto,"Nada");
}
}

void listarProductos() {
    for (i = 0; i < 100; i++) {
        printf("\n Id Producto->[%s]", tProductos[i].id_producto);
        printf("\n Descripcion->[%s]", tProductos[i].descripcion);
        printf("\n Precio Compra->[%.2f]", tProductos[i].precioCompra);
        printf("\n Precio Venta->[%.2f]", tProductos[i].precioVenta);
        printf("\n Existencia o Stoc->[%.2f]", tProductos[i].stock);
        printf("\n Unidad Medida->[%s]", tProductos[i].unidadMedida);
        printf("\n******************************************************");
    }
}

int buscarLugar() {
    for (i = 0; i < 100; i++) {
        if (strcmp(tProductos[i].id_producto, "Nada") == 0) {
            llave = i;
            return 1;
        }
    }
}

void pedirDatosProductos() {
    printf("\n\t\t\t\t\t Pedir Datos");
    printf("\n\t\t Dame Id del producto->");
    scanf("%s", &idP);
    fflush(stdin);
    printf("\n\t\t Dame La Descripcion->");
    scanf("%s", &des);
    fflush(stdin);
    printf("\n\t\t Dame la Unidad de Medida->");
    scanf("%s", &uM);
    fflush(stdin);
    printf("\n\t\t Dame precio de Compra->");
    scanf("%f", &pC);
    fflush(stdin);
    printf("\n\t\t Dame precio de Venta->");
    scanf("%f", &pV);
    fflush(stdin);
    printf("\n\t\t Dame Stock->");
    scanf("%f", &sT);
    fflush(stdin);
    printf("\n\t\t Dame la Clave del proveedor->");
    scanf("%s", &idPv);
    fflush(stdin);
}

void grabarDatosProductos(producto tProductos[], int llave, string idP, string des, string uM, float pC, float pV, float sT, string idPv) {
    strcpy(tProductos[llave].id_producto, idP);
    strcpy(tProductos[llave].descripcion, des);
    strcpy(tProductos[llave].unidadMedida, uM);
    strcpy(tProductos[llave].id_proveedor, idPv);
    tProductos[llave].precioCompra = pC;
    tProductos[llave].precioVenta = pV;
    tProductos[llave].stock = sT;
}

int buscarProducto(producto tProductos[], string idP) {
    for (i = 0; i < 100; i++) {
        if (strcmp(tProductos[i].id_producto, idP) == 0) {
            llave = i;
            return i;
        }
    }
}

void desplegarProducto(producto tProductos[]) {
    printf("\n\t\t 1.- Clave del Producto->[%s]", tProductos[llave].id_producto);
    printf("\n\t\t 2.- Descripción del Prodcuto->[%s]", tProductos[llave].descripcion);
    printf("\n\t\t 3.- Unidad de Medida->[%s]", tProductos[llave].unidadMedida);
    printf("\n\t\t 4.- Precio Compra->[%.2f]", tProductos[llave].precioCompra);
    printf("\n\t\t 5.- Precio Venta->[%.2f]", tProductos[llave].precioVenta);
    printf("\n\t\t 6.- Stock o Existencia->[%.2f]", tProductos[llave].stock);
    printf("\n\t\t 7.- Clave de Proveedor->[%s]", tProductos[llave].id_proveedor);
}

void bajaDatosProducto(producto tProductos[], int llave) {
    strcpy(tProductos[llave].id_producto, "Nada");
}

void listo() {
    printf("\n Listo Cambio Hecho Teclea Enter");
    getchar();
}
//clientes
void inicializaClientes() {
    for (i = 0; i < 20; i++) {
    tclientes[i].id_cliente=0;
    }
}

void listarClientes() {
    for (i = 0; i < 20; i++) {
        printf("\n Id Cliente->[%i]", tclientes[i].id_cliente);
        printf("\n Nombre->[%s]", tclientes[i].nombre);
        printf("\n Calle->[%s]", tclientes[i].calle);
        printf("\n Colonia->[%s]", tclientes[i].colonia);
        printf("\n Ciudad->[%s]", tclientes[i].ciudad);
        printf("\n Pais->[%s]", tclientes[i].pais);
        printf("\n Telefono->[%s]", tclientes[i].telefono);
        printf("\n Mail->[%s]", tclientes[i].mail);
        printf("\n******************************************************");
    }
}

void bajaDatosClientes(cliente tClientes[], int llave) {
    strcpy(tClientes[llave].id_cliente, "Nada");
}

void pedirDatosClientes() {
    printf("\n\t\t\t\t\t Pedir Datos");
    printf("\n\t\t Dame Id del cliente->");
    scanf("%i",&idC);
    fflush(stdin);
    printf("\n\t\t Dame Nombre->");
    scanf("%s", &nombre);
    fflush(stdin);
    printf("\n\t\t Dame Calle->");
    scanf("%s", &calle);
    fflush(stdin);
    printf("\n\t\t Dame Colonia->");
    scanf("%s", &colonia);
    fflush(stdin);
    printf("\n\t\t Dame Ciudad->");
    scanf("%s", &ciudad);
    fflush(stdin);
    printf("\n\t\t Dame Pais->");
    scanf("%s", &pais);
    fflush(stdin);
    printf("\n\t\t Dame Telefono->");
    scanf("%s", &telefono);
    fflush(stdin);
    printf("\n\t\t Dame Mail->");
    scanf("%s", &mail);
    fflush(stdin);
}

void grabarDatosClientes(cliente tClientes[], int llave, int idC, string nombre, string calle, string colonia, string ciudad, string pais, string telefono, string mail) {
    tClientes[llave].id_cliente = idC;
    strcpy(tClientes[llave].nombre, nombre);
    strcpy(tClientes[llave].calle, calle);
    strcpy(tClientes[llave].colonia, colonia);
    strcpy(tClientes[llave].ciudad, ciudad);
    strcpy(tClientes[llave].pais, pais);
    strcpy(tClientes[llave].telefono, telefono);
    strcpy(tClientes[llave].mail, mail);
}

int buscarClientes(cliente tClientes[], int idC) {
    for (int i = 0; i < 20; i++) {
        if (tClientes[i].id_cliente == idC) {
            llave = i;
            return i;
        }
    }
}

void desplegarClientes(cliente tClientes[]) {
    printf("\n\t\t 1.- Clave del Cliente->[%i]", tClientes[llave].id_cliente);
    printf("\n\t\t 2.- Nombre del Cliente->[%s]", tClientes[llave].nombre);
    printf("\n\t\t 3.- Calle->[%s]", tClientes[llave].calle);
    printf("\n\t\t 4.- Colonia->[%s]", tClientes[llave].colonia);
    printf("\n\t\t 5.- Ciudad->[%s]", tClientes[llave].ciudad);
    printf("\n\t\t 6.- Pais->[%s]", tClientes[llave].pais);
    printf("\n\t\t 7.- Telefono->[%s]", tClientes[llave].telefono);
    printf("\n\t\t 8.- Mail->[%s]", tClientes[llave].mail);
}
//provedores
void inicializaProveedores() {
    for (i = 0; i < 20; i++) {
        strcpy(tProveedores[i].id_proveedor, "Nada");
    }
}

void listarProveedores() {
    for (i = 0; i < 3; i++) {
        printf("\n Id Proveedor->[%s]", tProveedores[i].id_proveedor);
        printf("\n Nombre->[%s]", tProveedores[i].nombre);
        printf("\n Calle->[%.s]", tProveedores[i].calle);
        printf("\n Colonia->[%.s]", tProveedores[i].colonia);
        printf("\n Ciudad->[%.s]", tProveedores[i].ciudad);
        printf("\n Pais->[%s]", tProveedores[i].pais);
        printf("\n Telefono->[%s]", tProveedores[i].telefono);
        printf("\n Mail->[%s]", tProveedores[i].mail);
        printf("\n******************************************************");
    }
}

void bajaDatosProveedor(proveedor tProveedores[], int llave) {
    strcpy(tProveedores[llave].id_proveedor, "Nada");
}

void pedirDatosProveedor() {
    printf("\n\t\t\t\t\t Pedir Datos");
    printf("\n\t\t Dame Id del proveedor->");
    scanf("%s", &idP);
    fflush(stdin);
    printf("\n\t\t Dame Nombre->");
    scanf("%s", &des);
    fflush(stdin);
    printf("\n\t\t Dame Calle->");
    scanf("%s", &uM);
    fflush(stdin);
    printf("\n\t\t Dame Colonia->");
    scanf("%s", &pC);
    fflush(stdin);
    printf("\n\t\t Dame Ciudad->");
    scanf("%s", &pV);
    fflush(stdin);
    printf("\n\t\t Dame Pais->");
    scanf("%s", &sT);
    fflush(stdin);
    printf("\n\t\t Dame Telefono->");
    scanf("%s", &idPv);
    fflush(stdin);
    printf("\n\t\t Dame Mail->");
    scanf("%s", &idPv);
    fflush(stdin);
}

void grabarDatosProveedor(proveedor tProveedores[], int llave, string idPv, string nombre, string calle, string colonia, string ciudad, string pais, string telefono, string mail) {
    strcpy(tProveedores[llave].id_proveedor, idPv);
    strcpy(tProveedores[llave].nombre, nombre);
    strcpy(tProveedores[llave].calle, calle);
    strcpy(tProveedores[llave].colonia, colonia);
    strcpy(tProveedores[llave].ciudad, ciudad);
    strcpy(tProveedores[llave].pais, pais);
    strcpy(tProveedores[llave].telefono, telefono);
    strcpy(tProveedores[llave].mail, mail);
}

int buscarProveedor(proveedor tProveedores[], string idPv) {
    for (i = 0; i < 100; i++) {
        if (strcmp(tProveedores[i].id_proveedor, "nada")==0) {
            llave = i;
            return i;
        }
    }
}

void desplegarProveedor(proveedor tProveedores[]) {
    printf("\n\t\t 1.- id del Proveedor->[%s]", tProveedores[llave].id_proveedor);
    printf("\n\t\t 2.- Nombre del Proveedor->[%s]", tProveedores[llave].nombre);
    printf("\n\t\t 3.- Calle->[%s]", tProveedores[llave].calle);
    printf("\n\t\t 4.- Colonia->[%s]", tProveedores[llave].colonia);
    printf("\n\t\t 5.- Ciudad->[%s]", tProveedores[llave].ciudad);
    printf("\n\t\t 6.- Pais->[%s]", tProveedores[llave].pais);
    printf("\n\t\t 7.- Telefono->[%s]", tProveedores[llave].telefono);
    printf("\n\t\t 8.- Mail->[%s]", tProveedores[llave].mail);
}

void inicializaVentas() {
    for (i = 0; i < 1000; i++) {
        tVentas[i].id_venta = 0;
    }
}

void listarVentas() {
    for (i = 0; i < 1000; i++) {
        printf("\n Id Venta->[%i]", tVentas[i].id_venta);
        printf("\n Fecha->[%s]", tVentas[i].fecha);
        printf("\n Id Producto->[%s]", tVentas[i].id_producto);
        printf("\n Cantidad->[%.2f]", tVentas[i].cantidad);
        printf("\n Importe->[%.2f]", tVentas[i].importe);
        printf("\n Id Cliente->[%s]", tVentas[i].id_cliente);
        printf("\n******************************************************");
    }
}

void bajaDatosVentas(venta tVentas[], int llave) {
    tVentas[llave].id_venta = 0;
}

void pedirDatosVenta() {
    printf("\n\t\t\t\t\t Pedir Datos");
    printf("\n\t\t Dame Id de la venta->");
    scanf("%i",&idV);
    fflush(stdin);
    printf("\n\t\t Dame Fecha->");
    scanf("%s", &tVentas[llave].fecha);
    fflush(stdin);
    printf("\n\t\t Dame Id del Producto->");
    scanf("%s", &tVentas[llave].id_producto);
    fflush(stdin);
    printf("\n\t\t Dame Cantidad->");
    scanf("%f", &tVentas[llave].cantidad);
    fflush(stdin);
    printf("\n\t\t Dame Importe->");
    scanf("%f", &tVentas[llave].importe);
    fflush(stdin);
    printf("\n\t\t Dame Id del Cliente->");
    scanf("%s", &tVentas[llave].id_cliente);
    fflush(stdin);
}

void grabarDatosVenta(venta tVentas[], int llave, int idV, string fecha, string idP, float cantidad, float importe, string idC) {
    tVentas[llave].id_venta = idV;
    strcpy(tVentas[llave].fecha, fecha);
    strcpy(tVentas[llave].id_producto, idP);
    tVentas[llave].cantidad = cantidad;
    tVentas[llave].importe = importe;
    strcpy(tVentas[llave].id_cliente, idC);
}

int buscarVentas(venta tVentas[], int idV) {
    for (int i = 0; i < 1000; i++) {
        if (tVentas[i].id_venta == idV) {
            llave = i;
            return i;
        }
    }
}
void desplegarVenta(venta tVentas[]) {
    printf("\n\t\t 1.- Id Venta->[%i]", tVentas[llave].id_venta);
    printf("\n\t\t 2.- Fecha de la Venta->[%s]", tVentas[llave].fecha);
    printf("\n\t\t 3.- Id del Producto->[%s]", tVentas[llave].id_producto);
    printf("\n\t\t 4.- Cantidad Vendida->[%.2f]", tVentas[llave].cantidad);
    printf("\n\t\t 5.- Importe de la Venta->[%.2f]", tVentas[llave].importe);
    printf("\n\t\t 6.- Id del Cliente->[%s]", tVentas[llave].id_cliente);
}

//compras

void inicializaCompras() {
    for (i = 0; i < 1000; i++) {
    tCompras[i].id_compra=0;
    }
}

void listarCompras() {
    for (i = 0; i < 3; i++) {
        printf("\n Id Compra->[%i]", tCompras[i].id_compra);
        printf("\n Fecha->[%s]", tCompras[i].fecha);
        printf("\n Id Producto->[%s]", tCompras[i].id_producto);
        printf("\n Cantidad->[%.2f]", tCompras[i].cantidad);
        printf("\n Importe->[%.2f]", tCompras[i].importe);
        printf("\n Id Proveedor->[%s]", tCompras[i].id_proveedor);
        printf("\n******************************************************");
    }
}

void bajaDatosCompra(compra tCompras[], int llave) {
    strcpy(tCompras[i].id_compra, "nada");

}

void pedirDatosCompra() {
    printf("\n\t\t\t\t\t Pedir Datos");
    printf("\n\t\t Dame Id de la compra->");
    scanf("%i", &idC);
    fflush(stdin);
    printf("\n\t\t Dame Fecha->");
    scanf("%s", &tCompras[llave].fecha);
    fflush(stdin);
    printf("\n\t\t Dame Id del Producto->");
    scanf("%s", &tCompras[llave].id_producto);
    fflush(stdin);
    printf("\n\t\t Dame Cantidad->");
    scanf("%f", &tCompras[llave].cantidad);
    fflush(stdin);
    printf("\n\t\t Dame Importe->");
    scanf("%f", &tCompras[llave].importe);
    fflush(stdin);
    printf("\n\t\t Dame Id del Proveedor->");
    scanf("%s", &tCompras[llave].id_proveedor);
    fflush(stdin);
}

void grabarDatosCompra(compra tCompras[], int llave, int idC, string fecha, string idP, float cantidad, float importe, string idPv) {
    tCompras[i].id_compra, idC;
    strcpy(tCompras[llave].fecha, fecha);
    strcpy(tCompras[llave].id_producto, idP);
    tCompras[llave].cantidad = cantidad;
    tCompras[llave].importe = importe;
    strcpy(tCompras[llave].id_proveedor, idPv);
}

int buscarCompra(compra tCompras[], int idC) {
    for (i = 0; i < 1000; i++) {
        if (tCompras[i].id_compra == idC) {
            llave = i;
            return i;
        }
    }
}

void desplegarCompra(compra tCompras[]) {
    printf("\n\t\t 1.- Id Compra->[%i]", tCompras[llave].id_compra);
    printf("\n\t\t 2.- Fecha de la Compra->[%s]", tCompras[llave].fecha);
    printf("\n\t\t 3.- Id del Producto->[%s]", tCompras[llave].id_producto);
    printf("\n\t\t 4.- Cantidad Comprada->[%.2f]", tCompras[llave].cantidad);
    printf("\n\t\t 5.- Importe de la Compra->[%.2f]", tCompras[llave].importe);
    printf("\n\t\t 6.- Id del Proveedor->[%s]", tCompras[llave].id_proveedor);
}
