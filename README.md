#include <stdio.h>
#include <windows.h>
#include <string.h>
struct client{
	int id;
	char cedula[12];
	char nombre[30];
	char direccion[40];
	char telefono[30];
}cliente[100],*pcliente=cliente;
struct producto {
	int id;
	char nombre[30];
	float valor;
}productos[100],*pproducto=productos;
struct factura{
	int id;
	int id_cliente;
	int id_producto[100];
	int cantidad [100];
	float total;
	bool estado;
}facturas [100],*pfacturas=facturas;
int opcion=1,opc,i,j,cant_clientes=0,cant_productos=0,cant_facturas=0,cant,aux,pos,idclientes,idproductos,idfactura,aux_prec,comp_prod,var_aux[100],a,var_estado,k,res,z;
char aux_gen[40];
void gotoxy();
void Rectangulo(int, int);
void menu();
void punto_1(client *);
void crearcliente();
void mostrarcliente();
void editarclientes();
void punto_2(producto *);
void crearproductos();
void mostrarproductos();
void editarproducto();
void punto_3(factura *);
void crearfacturas();
void mostrarfacturas();
void editarfacturas();

void punto_5();

int main()
{
	menu();
	return 0;
}
void gotoxy(int x,int y )
{
	COORD coord;
	coord.X=x;
	coord.Y=y;
	SetConsoleCursorPosition( GetStdHandle(STD_OUTPUT_HANDLE),coord);
}
void Rectangulo(int altura, int ancho)
{
	int i;
	
	for (i=3;i<altura;i++)
	{
		gotoxy(2,i); printf("\263");
		gotoxy(ancho,i);printf("\263");
	}
	
	for (i=3;i<ancho;i++)
	{
		gotoxy(i,2); printf("\304");
		gotoxy(i,altura); printf("\304");
	}
	gotoxy(2,2); printf("\332"); 
	gotoxy(ancho,2); printf("\277"); 
	gotoxy(2,altura); printf("\300"); 
	gotoxy(ancho,altura); printf("\331"); 
}
void menu()
{		
	while(opcion!=0){
		Rectangulo(22,76);
		gotoxy(20,4);printf("S O F T W A R E  D E  F A C T U R A C I O N");
		gotoxy(15,8);printf( "1. Clientes");
		gotoxy(15,9);printf("2. Productos");
		gotoxy(15,10);printf("3. Facturas");
		gotoxy(15,11);printf("4. Visualizar Facturas");
		gotoxy(15,12);printf("5. Visualizar Clientes");
		gotoxy(15,13);printf("6. Visualizar Facturas Generadas por Clientes");
		gotoxy(15,14);printf("7. Visualizar Productos con cantidad vendida c/u");
		gotoxy(15,15);printf("8. Listas facturadas pagadas y sin pagar");
		gotoxy(15,17);printf("0. Salir ");
		gotoxy(15,19);printf("Seleccione Opcion: "); scanf("%d",&opcion);
		
		switch(opcion){
		case 1:
			punto_1(pcliente);
			break;
		case 2:
			punto_2(pproducto);
			break;
		case 3:
			punto_3(pfacturas);
			break;
		case 4:
			break;
		case 5:
			system("cls");
			punto_5();
			system("pause");
			system("cls");
			break;
		case 0: {
			system("CLS");
			Rectangulo(22,76);
			gotoxy(20,7);printf("SALIR");
			break;
		}          
		default:{
			system("CLS");
			Rectangulo(22,76);
			gotoxy(20,7);printf("Opcion no valida\n");
			system("pause");
			system("cls");
			break;
		} 
		}
	}
}
void punto_1(client *pcliente)
{
	system("cls");
	Rectangulo(22,76);
	gotoxy(30,4);printf("C L I E N T E S");
	gotoxy(15,8);printf( "1. Crear");
	gotoxy(15,9);printf("2. Listar");
	gotoxy(15,10);printf("3. Editar");
	gotoxy(15,12);printf("Seleccione Opcion: ");scanf("%d",&opc);
	switch(opc){
	case 1:
		system("cls");
		Rectangulo(22,76);
		crearcliente();
		system("pause");
		system("cls");
		break;
	case 2:
		system("cls");
		mostrarcliente();
		system("pause");
		system("cls");
		break;
	case 3:
		system("cls");
		Rectangulo(22,76);
		editarclientes();
		system("pause");
		system("cls");
		break;
	}
}
void crearcliente()
{
	Rectangulo(22,76);
	gotoxy(15,6);printf("Ingrese la Cantidad de Clientes: ");
	scanf("%d",&cant);
	system("cls");
	fflush(stdin);
	
	for(i=cant_clientes+1;i<=cant+cant_clientes;i++){
		(pcliente+i)->id=i;
		Rectangulo(22,76);
		gotoxy(15,4);printf( "Cliente: %d ",(pcliente+i)->id);
		gotoxy(15,6);printf( "Cedula Cliente: ");
		gotoxy(15,7);scanf("%s",&(pcliente+i)->cedula);
		fflush(stdin);
		gotoxy(15,8);printf( "Nombre Cliente: ");
		gotoxy(15,9);fgets((pcliente+i)->nombre,30,stdin);
		gotoxy(15,10);printf( "Direccion Cliente: ");
		gotoxy(15,11);fgets((pcliente+i)->direccion,40,stdin);
		gotoxy(15,12);printf( "Telefono Cliente: ");
		gotoxy(15,13);scanf("%s",&(pcliente+i)->telefono);
		fflush(stdin);
		system("cls");
		
	}
	cant_clientes=cant_clientes+cant;
	
}
void mostrarcliente()
{
	for(i=1;i<=cant_clientes;i++){
		printf("\n_________________________\n\n");	
		printf( "Id: %d \n",(pcliente+i)->id);
		printf( "Cedula Cliente: %s \n",(pcliente+i)->cedula);
		printf( "Nombre Cliente: %s ",(pcliente+i)->nombre );
		printf( "Direccion Cliente: %s",(pcliente+i)->direccion);
		printf( "Telefono Cliente: %s\n ",(pcliente+i)->telefono);
		printf("\n_________________________\n\n");
	}
}
void editarclientes()
{
	Rectangulo(22,76);
	gotoxy(15,4);printf("Ingrese el Id del Cliente que desea editar: ");
	scanf("%d",&idclientes);
	system("cls");
	for(i=1;i<=cant_clientes;i++){
		if((pcliente+i)->id==idclientes){
			Rectangulo(22,76);
			gotoxy(15,7);printf( "Id: %d \n",(pcliente+i)->id);
			gotoxy(15,8);printf( "1. Cedula Cliente: %s ",(pcliente+i)->cedula);
			gotoxy(15,9);printf( "2. Nombre Cliente: %s ",(pcliente+i)->nombre );
			gotoxy(15,10);printf( "3. Direccion Cliente: %s",(pcliente+i)->direccion);
			gotoxy(15,11);printf( "4. Telefono Cliente: %s ",(pcliente+i)->telefono);
			gotoxy(15,13);printf( "Que campo desea cambiar : ");
			gotoxy(43,13);scanf( "%d",&aux);
			fflush(stdin);
			if(aux==1){
				Rectangulo(22,76);
				gotoxy(15,14);printf("Ingrese la nueva cedula: ");
				gotoxy(43,14);fgets(aux_gen,40,stdin);
				strcpy((pcliente+i)->cedula,aux_gen);
				gotoxy(15,16);printf( "Nueva Cedula Cliente: %s",(pcliente+i)->cedula);
			}else{
				if(aux==2){
					Rectangulo(22,76);
					gotoxy(15,14);printf("Ingrese el nuevo nombre: ");
					gotoxy(43,14);fgets(aux_gen,40,stdin);
					strcpy((pcliente+i)->nombre,aux_gen);
					gotoxy(15,16);printf( "Nuevo Nombre Cliente: %s",(pcliente+i)->nombre);
				}else{
					if(aux==3){
						Rectangulo(22,76);
						gotoxy(15,14);printf("Ingrese la nueva direccion: ");
						gotoxy(43,14);fgets(aux_gen,40,stdin);
						strcpy((pcliente+i)->direccion,aux_gen);
						gotoxy(15,16);printf( "Nuevo Nombre Cliente: %s",(pcliente+i)->direccion);
					}else{
						if(aux==4){
							Rectangulo(22,76);
							gotoxy(15,14);printf("Ingrese el nuevo telefono: ");
							gotoxy(43,14);fgets(aux_gen,40,stdin);
							strcpy((pcliente+i)->telefono,aux_gen);
							gotoxy(15,16);printf( "Nuevo Nombre Cliente: %s",(pcliente+i)->telefono);
						}
					}
				}
			}
		}
	}
	Rectangulo(22,76);
	
	
	
}

void punto_2(producto *pproducto)
{
	system("cls");
	Rectangulo(22,76);
	gotoxy(30,4);printf("P R O D U C T O S");
	gotoxy(15,8);printf( "1. Crear");
	gotoxy(15,9);printf("2. Listar");
	gotoxy(15,10);printf("3. Editar");
	gotoxy(15,12);printf("Seleccione Opcion: ");scanf("%d",&opc);
	switch(opc){
	case 1:
		system("cls");
		Rectangulo(22,76);
		crearproductos();
		system("pause");
		system("cls");
		break;
	case 2:
		system("cls");
		mostrarproductos();
		system("pause");
		system("cls");
		break;
	case 3:
		system("cls");
		Rectangulo(22,76);
		editarproducto();
		system("pause");
		system("cls");
		break;
	}
}
void crearproductos()
{
	Rectangulo(22,76);
	gotoxy(15,6);printf("Ingrese la Cantidad de Productos: ");
	scanf("%d",&cant);
	system("cls");
	fflush(stdin);
	for(i=cant_productos+1;i<=cant+cant_productos;i++){
		(pproducto+i)->id=(pproducto+i)->id+i;
		Rectangulo(22,76);
		fflush(stdin);
		gotoxy(15,6);printf( "Nombre Producto: ");
		gotoxy(15,7);fgets((pproducto+i)->nombre,30,stdin);
		gotoxy(15,8);printf( "Valor Producto: ");
		gotoxy(15,9);scanf("%f",&(pproducto+i)->valor);
		fflush(stdin);
		system("cls");
		
	}
	cant_productos=cant_productos+cant;
	
}
void mostrarproductos()
{
	for(i=1;i<=cant_productos;i++){
		printf("\n_________________________\n\n");	
		printf( "Id: %d \n",(pproducto+i)->id);
		printf( "Nombre Producto: %s ",(pproducto+i)->nombre);
		printf( "Valor: %.f ",(pproducto+i)->valor );
		printf("\n_________________________\n\n");
	}
}
void editarproducto()
{
	Rectangulo(22,76);
	gotoxy(15,4);printf("Ingrese el Id del Producto que desea editar: ");
	scanf("%d",&idproductos);
	system("cls");
	for(i=1;i<=cant_productos;i++){
		if((pproducto+i)->id==idproductos){
			Rectangulo(22,76);
			gotoxy(15,7);printf( "Id: %d \n",(pproducto+i)->id);
			gotoxy(15,8);printf( "1. Nombre Producto: %s ",(pproducto+i)->nombre);
			gotoxy(15,9);printf( "2. Valor Producto: %.f ",(pproducto+i)->valor );
			gotoxy(15,13);printf( "Que campo desea cambiar : ");
			gotoxy(43,13);scanf( "%d",&aux);
			fflush(stdin);
			if(aux==1){
				Rectangulo(22,76);
				gotoxy(15,14);printf("Ingrese el nuevo Nombre del Producto: ");
				gotoxy(15,15);fgets(aux_gen,30,stdin);
				strcpy((pproducto+i)->nombre,aux_gen);
				gotoxy(15,16);printf( "Nuevo Nombre Producto: %s",(pproducto+i)->nombre);
			}else{
				if(aux==2){
					Rectangulo(22,76);
					gotoxy(15,14);printf("Ingrese el nuevo Valor: ");
					gotoxy(43,14);scanf("%f",&aux_prec);
					((pproducto+i)->valor=aux_prec);
					gotoxy(15,16);printf( "Nuevo Precio Producto: %.f",(pcliente+i)->nombre);
				}
			}
		}
	}
	Rectangulo(22,76);
	
}
void punto_3(factura *pfacturas)
{
	system("cls");
	Rectangulo(22,76);
	gotoxy(30,4);printf("F A C T U R A S");
	gotoxy(15,8);printf( "1. Crear");
	gotoxy(15,9);printf("2. Listar");
	gotoxy(15,10);printf("3. Editar");
	gotoxy(15,12);printf("Seleccione Opcion: ");scanf("%d",&opc);
	switch(opc){
	case 1:
		system("cls");
		crearfacturas();
		gotoxy(6,24); system("pause");
		system("cls");
		break;
	case 2:
		system("cls");
		mostrarfacturas();
		system("cls");
		break;
	case 3:
		system("cls");
		Rectangulo(22,76);
		editarfacturas();
		gotoxy(6,26);system("pause");
		system("cls");
		break;
	}
}


void crearfacturas()
{
	printf("ingrese la cantidad de facturas que va a ingresar: ");
	scanf("%d",&cant);
	for(z=cant_facturas+1;z<=cant+cant_facturas;z++){
		(pfacturas+z)->id=(pfacturas+z)->id+z;
		for(i=1;i<=cant_clientes;i++){	
			gotoxy(5,i);printf( "Id: %d \t Nombre Cliente: %s ",(pcliente+i)->id,(pcliente+i)->nombre );
		}
		for(i=1;i<=cant_productos;i++){	
			gotoxy(40,i);printf( "Id: %d \t Producto: %s ",(pproducto+i)->id,(pproducto+i)->nombre );
			
		}
		
		printf("\nIngrese el id del Cliente que busca: ");
		scanf("%d",&(pfacturas+z)->id_cliente);
		
		for(i=1;i<=cant_productos;i++){
			printf("\nIngrese el id del producto que busca: ");
			scanf("%d",&(pfacturas+z)->id_producto[i]);
			printf("ingrese la cantidad: ");
			scanf("%d",&(pfacturas+z)->cantidad[i]);
			printf("\nDesea agregar otro producto 1.Si / 2. No: ");
			scanf("%d",&comp_prod);
			if(comp_prod==2){
				break;
			}
		}
		printf("La factura ha sido cancelada ? 1. SI / 0. NO : ");
		scanf("%d",&(pfacturas+z)->estado);
		
		fflush(stdin);
		system("cls");
		for(i=1;i<=cant_clientes;i++){
			if((pfacturas+z)->id_cliente==(pcliente+i)->id){
				Rectangulo(22,76);
				gotoxy(6,4);printf( "Cliente: %s ",(pcliente+i)->nombre );	
				gotoxy(6,5);printf( "Cedula Cliente: %s ",(pcliente+i)->cedula);
				gotoxy(6,6);printf( "Direccion Cliente: %s",(pcliente+i)->direccion);
				gotoxy(6,7);printf( "Telefono Cliente: %s ",(pcliente+i)->telefono);
			}
		}
		for(i = 1; i <= cant_productos; i++)
		{
			for(j = i+1; j <= cant_productos; j++)
			{
				if(  (pfacturas+z)->id_producto[j] < (pfacturas+z)->id_producto[i] ){
					aux = (pfacturas+i)->id_producto[j];
					(pfacturas+z)->id_producto[j] = (pfacturas+z)->id_producto[i];
					(pfacturas+z)->id_producto[i] = (pfacturas+z)->id_producto[j];
					(pfacturas+z)->id_producto[i] = aux;
				}
			}
		}	
		
		for(i = 1; i <= cant_productos; i++)
		{
			for(j = i+1; j <= cant_productos; j++)
			{
				if(  (pfacturas+z)->cantidad[j] < (pfacturas+z)->cantidad[i] ){
					aux = (pfacturas+i)->cantidad[j];
					(pfacturas+z)->cantidad[j] = (pfacturas+z)->cantidad[i];
					(pfacturas+z)->cantidad[i] = (pfacturas+z)->cantidad[j];
					(pfacturas+z)->cantidad[i] = aux;
				}
			}
		}
		gotoxy(6,9);printf( "Productos \t cantidad \t Vlr/unit.  \t total ");
		k=10;
		for(i=1;i<=cant_productos;i++){
			if((pfacturas+z)->id_producto[i]==(pproducto+i)->id){
				(pfacturas+z)->total=(pfacturas+z)->cantidad[i]*(pproducto+i)->valor;
				gotoxy(6,k);printf( " %s ",(pproducto+i)->nombre);
				gotoxy(28,k);printf("%d",(pfacturas+i)->cantidad[i]);
				gotoxy(42,k);printf("%.f ",(pproducto+i)->valor);
				gotoxy(57,k);printf(" %.f ",(pfacturas+i)->total);
				if((pfacturas+i)->estado==true){
					gotoxy(50,4);printf( " FACTURA %d : CANCELADA ",(pfacturas+z)->id);
				}
				if((pfacturas+i)->estado==false){
					gotoxy(50,4);printf( " FACTURA %d : SIN CANCELAR ",(pfacturas+z)->id);
				}
				k++;
			}
		}
		
		gotoxy(6,24); system("pause");
		system("cls");
	}
	cant_facturas=cant_facturas+cant;
	
}
void mostrarfacturas()
{
	for(z=1;z<=cant_facturas;z++){
		
		for(i=1;i<=cant_clientes;i++){
			if((pfacturas+z)->id_cliente==(pcliente+i)->id){
				Rectangulo(22,76);
				gotoxy(6,4);printf( "Cliente: %s ",(pcliente+i)->nombre );	
				gotoxy(6,5);printf( "Cedula Cliente: %s ",(pcliente+i)->cedula);
				gotoxy(6,6);printf( "Direccion Cliente: %s",(pcliente+i)->direccion);
				gotoxy(6,7);printf( "Telefono Cliente: %s ",(pcliente+i)->telefono);
			}
		}
		
		gotoxy(6,9);printf( "Productos \t cantidad \t Vlr/unit.  \t total ");
		k=10;
		for(i=1;i<=cant_productos;i++){
			if((pfacturas+z)->id_producto[i]==(pproducto+i)->id){
				(pfacturas+z)->total=(pfacturas+z)->cantidad[i]*(pproducto+i)->valor;
				gotoxy(6,k);printf( " %s ",(pproducto+i)->nombre);
				gotoxy(28,k);printf("%d",(pfacturas+i)->cantidad[i]);
				gotoxy(42,k);printf("%.f ",(pproducto+i)->valor);
				gotoxy(57,k);printf(" %.f ",(pfacturas+i)->total);
				if((pfacturas+i)->estado==true){
					gotoxy(50,4);printf( " FACTURA %d : CANCELADA ",(pfacturas+z)->id);
				}
				if((pfacturas+i)->estado==false){
					gotoxy(50,4);printf( "FACTURA %d : SIN CANCELAR ",(pfacturas+z)->id);
				}
				k++;
			}
		}
		if( cant_facturas > 1 ){
			gotoxy(6,24);printf("Oprima Enter Para ver Otra Factura");
		}
		gotoxy(6,25); system("pause");
		system("cls");
		
	}
	
}
void editarfacturas(){
	gotoxy(6,1);printf("Ingrese el ID de la factura: ");
	scanf("%d",&idfactura);
	system("cls");
	for (z=1;z<=cant_facturas;z++){
		if((pfacturas+z)->id==idfactura){
			for(i=1;i<=cant_clientes;i++){
				if((pfacturas+z)->id_cliente==(pcliente+i)->id){
					Rectangulo(22,76);
					gotoxy(6,4);printf( "1.Cliente: %s ",(pcliente+i)->nombre );	
					gotoxy(6,5);printf( "2.Cedula Cliente: %s ",(pcliente+i)->cedula);
					gotoxy(6,6);printf( "3.Direccion Cliente: %s",(pcliente+i)->direccion);
					gotoxy(6,7);printf( "4.Telefono Cliente: %s ",(pcliente+i)->telefono);
				}
			}
			
			gotoxy(6,9);printf( "6. Productos \t 7. cantidad \t 8. Vlr/unit.  \t  total ");
			k=10;
			for(i=1;i<=cant_productos;i++){
				if((pfacturas+z)->id_producto[i]==(pproducto+i)->id){
					(pfacturas+i)->total=(pfacturas+z)->cantidad[i]*(pproducto+i)->valor;
					gotoxy(6,k);printf( " %s ",(pproducto+i)->nombre);
					gotoxy(28,k);printf("%d",(pfacturas+i)->cantidad[i]);
					gotoxy(42,k);printf("%.f ",(pproducto+i)->valor);
					gotoxy(57,k);printf(" %.f ",(pfacturas+i)->total);
					if((pfacturas+i)->estado==true){
						gotoxy(50,4);printf( "5. FACTURA %d : CANCELADA ",(pfacturas+z)->id);
					}
					if((pfacturas+i)->estado==false){
						gotoxy(50,4);printf( "5. FACTURA %d : SIN CANCELAR ",(pfacturas+z)->id);
					}
					k++;
				}
				gotoxy(6,1);printf("Ingrese el numero del campo que desea editar(del 1 al 8): ");
				gotoxy(66,1);scanf("%d",&aux);
				system("cls");
				fflush(stdin);
				switch(aux){
				case 1:
					gotoxy(6,1);printf("Ingrese el Nuevo Nombre: ");
					gotoxy(32,1);fgets(aux_gen,40,stdin);
					strcpy((pcliente+i)->nombre,aux_gen);
					break;
				case 2:
					gotoxy(6,1);printf("Ingrese la nueva cedula: ");
					gotoxy(32,1);scanf("%s",aux_gen);
					strcpy((pcliente+i)->cedula,aux_gen);
					break;	
				case 3:
					gotoxy(6,1);printf("Ingrese la nueva direccion: ");
					gotoxy(36,1);fgets(aux_gen,40,stdin);
					strcpy((pcliente+i)->direccion,aux_gen);
					break;
				case 4:
					gotoxy(6,1);printf("Ingrese el nuevo telefono: ");
					gotoxy(34,1);scanf("%s",aux_gen);
					strcpy((pcliente+i)->telefono,aux_gen);
					break;
				case 5:
					if((pfacturas+i)->estado==1){
						(pfacturas+i)->estado=0;
					}else{
						if((pfacturas+i)->estado==0){
							(pfacturas+i)->estado=1;
						}
					}
					gotoxy(6,25);printf("campo editado");
					break;
				case 6:
					gotoxy(6,1);printf("Ingrese el nuevo Nombre del Producto: ");
					gotoxy(44,1);fgets(aux_gen,30,stdin);
					strcpy((pproducto+i)->nombre,aux_gen);
					break;
				case 7:
					gotoxy(6,1);printf("Ingrese la nueva cantidad: ");
					gotoxy(34,1);scanf("%d",&(pfacturas+z)->cantidad[i]);					
					break;
				case 8:
					gotoxy(6,1);printf("Ingrese el nuevo Valor: ");
					gotoxy(32,1);scanf("%f",&aux_prec);
					(pproducto+i)->valor=aux_prec;
					break;
				}
				(pfacturas+i)->total=(pfacturas+z)->cantidad[i]*(pproducto+i)->valor;
			}
			
		}
	}
}
void punto_5()
{
	for(i=1;i<=cant_clientes;i++){
		printf("\n_________________________\n\n");	
		printf( "Id: %d \n",(pcliente+i)->id);
		printf( "Cedula Cliente: %s \n",(pcliente+i)->cedula);
		printf( "Nombre Cliente: %s ",(pcliente+i)->nombre );
		printf( "Direccion Cliente: %s",(pcliente+i)->direccion);
		printf( "Telefono Cliente: %s\n ",(pcliente+i)->telefono);
		printf("\n_________________________\n\n");
	}
	system("pause");
	system("cls");
}

