//нахождение точки пересечения двух отрезков в пространстве
#include<iostream>
#include<string>
#include<stdio.h>
#include<conio.h>

using namespace std;

class Vector3D
{
public:
	double X;
	double Y;
	double Z;
	
	Vector3D() {}

	Vector3D(double x, double y, double z)
	{
		X = x;
		Y = y;
		Z = z;
	}


	Vector3D DivideOnK(double K)
	{
		Vector3D DivideOnKVector (X / K, Y / K, Z / K);
		return DivideOnKVector;
	}

};

class Segment3D
{
public:
	Vector3D start;
	Vector3D end;

	Segment3D() {}

	Segment3D(Vector3D Start, Vector3D End)
	{
		start = Start;
		end = End;
	}

	Vector3D napr()
	{
		double x = end.X - start.X;
		double y = end.Y - start.Y;
		double z = end.Z - start.Z;
		Vector3D Diff = Vector3D::Vector3D(x, y, z);
		return Diff;
	}

};

bool RavenstvoVectorov(Vector3D Vector1, Vector3D Vector2)
{
	if ((Vector1.X == Vector2.X) && (Vector1.Y == Vector2.Y) && (Vector1.Z == Vector2.Z))
		return true;
	return false;
}

bool OdnaPloskost(Segment3D AB, Segment3D CD)
{	
	double x[4], y[4], z[4];

	x[0] = AB.start.X;
	y[0] = AB.start.Y;
	z[0] = AB.start.Z;
	
	x[1] = AB.end.X;
	y[1] = AB.end.Y;
	z[1] = AB.end.Z;

	x[2] = CD.start.X;
	y[2] = CD.start.Y;
	z[2] = CD.start.Z;

	x[3] = CD.end.X;
	y[3] = CD.end.Y;
	z[3] = CD.end.Z;


	double A[3][3];

/*
	A[0][0] = x[3] - x[0];
	A[1][0] = y[3] - y[0];
	A[2][0] = z[3] - z[0];

	A[0][1] = x[1] - x[0];
	A[1][1] = y[1] - y[0];
	A[2][1] = z[1] - z[0];

	A[0][2] = x[2] - x[0];
	A[1][2] = y[2] - y[0];
	A[2][2] = z[2] - z[0];
*/
	//записывем в цикл, переставляя два раза 2 строки, определитель не меняется

	for (int i = 0; i < 3; i++)
	{
		A[0][i] = x[i+1] - x[0];
		A[1][i] = y[i+1] - y[0];
		A[2][i] = z[i+1] - z[0];

	}

	//cout << A[0][0] << " " << A[0][1] << " " << A[0][2] << endl;
	//cout << A[1][0] << " " << A[1][1] << " " << A[1][2] << endl;
	//cout << A[2][0] << " " << A[2][1] << " " << A[2][2] << endl;


	//считаем определитель матрицы A
	double Opr = A[0][0]* A[1][1] * A[2][2] + A[0][1] * A[1][2] * A[2][0] + A[0][2] * A[1][0] * A[2][1] - A[0][2] * A[1][1] * A[2][0] - A[0][0] * A[1][2] * A[2][1] - A[0][1] * A[1][0] * A[2][2];
	//cout << "определитель: " << Opr << endl;

	if (Opr == 0)
	{
		return true;
	}
	else
	{
		return false;
	}
}


Vector3D* PoiskTochki(Segment3D AB, Segment3D CD)
{
	// два отрезка лежат в одной плоскости и они не параллельны
	Vector3D naprAB = AB.napr();
	Vector3D naprCD = CD.napr();
	
	//x0 = naprAB.X * t0 + AB.start.X = naprCD.X * s0 + CD.start.X;
	//y0 = naprAB.Y * t0 + AB.start.Y = naprCD.Y * s0 + CD.start.Y;
	//z0 = naprAB.Z * t0 + AB.start.Z = naprCD.Z * s0 + CD.start.Z;
	
	//t0 = (naprCD.X * s0 + CD.start.X - AB.start.X) / naprAB.X; Если naprAB.X не равно 0

	// naprAB.Y * (naprCD.X * s0 + CD.start.X - AB.start.X) / naprAB.X + AB.start.Y = naprCD.Y * s0 + CD.start.Y;
	// naprAB.Z * (naprCD.X * s0 + CD.start.X - AB.start.X) / naprAB.X + AB.start.Z = naprCD.Z * s0 + CD.start.Z;

	// naprAB.Y * naprCD.X * s0 / naprAB.X + naprAB.Y * (CD.start.X - AB.start.X) / naprAB.X + AB.start.Y = naprCD.Y * s0 + CD.start.Y;
	// naprAB.Z * naprCD.X * s0 / naprAB.X + naprAB.Z * (CD.start.X - AB.start.X) / naprAB.X + AB.start.Z = naprCD.Z * s0 + CD.start.Z;

	// naprAB.Y * naprCD.X / naprAB.X * s0 - naprCD.Y * s0 + naprAB.Y * (CD.start.X - AB.start.X) / naprAB.X + AB.start.Y = CD.start.Y;
	// naprAB.Z * naprCD.X / naprAB.X * s0 - naprCD.Z * s0 + naprAB.Z * (CD.start.X - AB.start.X) / naprAB.X + AB.start.Z = CD.start.Z;

	// ( naprAB.Y * naprCD.X / naprAB.X - naprCD.Y ) * s0 + naprAB.Y * (CD.start.X - AB.start.X) / naprAB.X + AB.start.Y = CD.start.Y;
	// ( naprAB.Z * naprCD.X / naprAB.X - naprCD.Z ) * s0 + naprAB.Z * (CD.start.X - AB.start.X) / naprAB.X + AB.start.Z = CD.start.Z;

	// s0 = ( CD.start.Y - naprAB.Y * (CD.start.X - AB.start.X) / naprAB.X - AB.start.Y ) / ( naprAB.Y * naprCD.X / naprAB.X - naprCD.Y ); Если naprAB.Y * naprCD.X / naprAB.X - naprCD.Y не равно 0
	// s0 = ( CD.start.Z - naprAB.Z * (CD.start.X - AB.start.X) / naprAB.X - AB.start.Z ) / ( naprAB.Z * naprCD.X / naprAB.X - naprCD.Z ); Если naprAB.Z * naprCD.X / naprAB.X - naprCD.Z не равно 0	

	if (naprAB.X != 0)
	{
		if (naprAB.Y * naprCD.X / naprAB.X - naprCD.Y != 0)
		{
			double s0 = (CD.start.Y - naprAB.Y * (CD.start.X - AB.start.X) / naprAB.X - AB.start.Y) / (naprAB.Y * naprCD.X / naprAB.X - naprCD.Y);
			
			double x0 = naprCD.X * s0 + CD.start.X;
			double y0 = naprCD.Y * s0 + CD.start.Y;
			double z0 = naprCD.Z * s0 + CD.start.Z;


			Vector3D* P = new Vector3D(x0, y0, z0); //точка пересечения отрезков

			return P;
		}
		
		if (naprAB.Z * naprCD.X / naprAB.X - naprCD.Z != 0)
		{
			double s0 = (CD.start.Z - naprAB.Z * (CD.start.X - AB.start.X) / naprAB.X - AB.start.Z) / (naprAB.Z * naprCD.X / naprAB.X - naprCD.Z);

			double x0 = naprCD.X * s0 + CD.start.X;
			double y0 = naprCD.Y * s0 + CD.start.Y;
			double z0 = naprCD.Z * s0 + CD.start.Z;


			Vector3D* P = new Vector3D(x0, y0, z0); //точка пересечения отрезков

			return P;
		}

	}



	//x0 = naprAB.X * t0 + AB.start.X = naprCD.X * s0 + CD.start.X;
	//y0 = naprAB.Y * t0 + AB.start.Y = naprCD.Y * s0 + CD.start.Y;
	//z0 = naprAB.Z * t0 + AB.start.Z = naprCD.Z * s0 + CD.start.Z;

	//t0 = (naprCD.Y * s0 + CD.start.Y - AB.start.Y) / naprAB.Y; Если naprAB.Y не равно 0

	// naprAB.X * (naprCD.Y * s0 + CD.start.Y - AB.start.Y) / naprAB.Y + AB.start.X = naprCD.X * s0 + CD.start.X;
	// naprAB.Z * (naprCD.Y * s0 + CD.start.Y - AB.start.Y) / naprAB.Y + AB.start.Z = naprCD.Z * s0 + CD.start.Z;

	// naprAB.X * naprCD.Y * s0 / naprAB.Y + naprAB.X * (CD.start.Y - AB.start.Y) / naprAB.Y + AB.start.X = naprCD.X * s0 + CD.start.X;
	// naprAB.Z * naprCD.Y * s0 / naprAB.Y + naprAB.Z * (CD.start.Y - AB.start.Y) / naprAB.Y + AB.start.Z = naprCD.Z * s0 + CD.start.Z;

	// naprAB.X * naprCD.Y / naprAB.Y * s0 - naprCD.X * s0 + naprAB.X * (CD.start.Y - AB.start.Y) / naprAB.Y + AB.start.X = CD.start.X;
	// naprAB.Z * naprCD.Y / naprAB.Y * s0 - naprCD.Z * s0 + naprAB.Z * (CD.start.Y - AB.start.Y) / naprAB.Y + AB.start.Z = CD.start.Z;

	// ( naprAB.X * naprCD.Y / naprAB.Y - naprCD.X ) * s0 + naprAB.X * (CD.start.Y - AB.start.Y) / naprAB.Y + AB.start.X = CD.start.X;
	// ( naprAB.Z * naprCD.Y / naprAB.Y - naprCD.Z ) * s0 + naprAB.Z * (CD.start.Y - AB.start.Y) / naprAB.Y + AB.start.Z = CD.start.Z;

	// s0 = ( CD.start.X - naprAB.X * (CD.start.Y - AB.start.Y) / naprAB.Y - AB.start.X ) / ( naprAB.X * naprCD.Y / naprAB.Y - naprCD.X ); Если naprAB.X * naprCD.Y / naprAB.Y - naprCD.X не равно 0
	// s0 = ( CD.start.Z - naprAB.Z * (CD.start.Y - AB.start.Y) / naprAB.Y - AB.start.Z ) / ( naprAB.Z * naprCD.Y / naprAB.Y - naprCD.Z ); Если naprAB.Z * naprCD.Y / naprAB.Y - naprCD.Z не равно 0	

	
	if (naprAB.Y != 0)
	{
		if (naprAB.X * naprCD.Y / naprAB.Y - naprCD.X != 0)
		{
			double s0 = (CD.start.X - naprAB.X * (CD.start.Y - AB.start.Y) / naprAB.Y - AB.start.X) / (naprAB.X * naprCD.Y / naprAB.Y - naprCD.X);
			
			double x0 = naprCD.X * s0 + CD.start.X;
			double y0 = naprCD.Y * s0 + CD.start.Y;
			double z0 = naprCD.Z * s0 + CD.start.Z;


			Vector3D* P = new Vector3D(x0, y0, z0); //точка пересечения отрезков

			return P;
		}
		
		if (naprAB.Z * naprCD.Y / naprAB.Y - naprCD.Z != 0)
		{
			double s0 = (CD.start.Z - naprAB.Z * (CD.start.Y - AB.start.Y) / naprAB.Y - AB.start.Z) / (naprAB.Z * naprCD.Y / naprAB.Y - naprCD.Z);

			double x0 = naprCD.X * s0 + CD.start.X;
			double y0 = naprCD.Y * s0 + CD.start.Y;
			double z0 = naprCD.Z * s0 + CD.start.Z;


			Vector3D* P = new Vector3D(x0, y0, z0); //точка пересечения отрезков

			return P;
		}

	}



	//x0 = naprAB.X * t0 + AB.start.X = naprCD.X * s0 + CD.start.X;
	//y0 = naprAB.Y * t0 + AB.start.Y = naprCD.Y * s0 + CD.start.Y;
	//z0 = naprAB.Z * t0 + AB.start.Z = naprCD.Z * s0 + CD.start.Z;
	
	//t0 = (naprCD.Z * s0 + CD.start.Z - AB.start.Z) / naprAB.Z; Если naprAB.Z не равно 0

	// naprAB.X * (naprCD.Z * s0 + CD.start.Z - AB.start.Z) / naprAB.Z + AB.start.X = naprCD.X * s0 + CD.start.X;
	// naprAB.Y * (naprCD.Z * s0 + CD.start.Z - AB.start.Z) / naprAB.Z + AB.start.Y = naprCD.Y * s0 + CD.start.Y;

	// naprAB.X * naprCD.Z * s0 / naprAB.Z + naprAB.X * (CD.start.Z - AB.start.Z) / naprAB.Z + AB.start.X = naprCD.X * s0 + CD.start.X;
	// naprAB.Y * naprCD.Z * s0 / naprAB.Z + naprAB.Y * (CD.start.Z - AB.start.Z) / naprAB.Z + AB.start.Y = naprCD.Y * s0 + CD.start.Y;

	// naprAB.X * naprCD.Z / naprAB.Z * s0 - naprCD.X * s0 + naprAB.X * (CD.start.Z - AB.start.Z) / naprAB.Z + AB.start.X = CD.start.X;
	// naprAB.Y * naprCD.Z / naprAB.Z * s0 - naprCD.Y * s0 + naprAB.Y * (CD.start.Z - AB.start.Z) / naprAB.Z + AB.start.Y = CD.start.Y;

	// ( naprAB.X * naprCD.Z / naprAB.Z - naprCD.X ) * s0 + naprAB.X * (CD.start.Z - AB.start.Z) / naprAB.Z + AB.start.X = CD.start.X;
	// ( naprAB.Y * naprCD.Z / naprAB.Z - naprCD.Y ) * s0 + naprAB.Y * (CD.start.Z - AB.start.Z) / naprAB.Z + AB.start.Y = CD.start.Y;

	// s0 = ( CD.start.X - naprAB.X * (CD.start.Z - AB.start.Z) / naprAB.Z - AB.start.X ) / ( naprAB.X * naprCD.Z / naprAB.Z - naprCD.X ); Если naprAB.X * naprCD.Z / naprAB.Z - naprCD.X не равно 0
	// s0 = ( CD.start.Y - naprAB.Y * (CD.start.Z - AB.start.Z) / naprAB.Z - AB.start.Y ) / ( naprAB.Y * naprCD.Z / naprAB.Z - naprCD.Y ); Если naprAB.Y * naprCD.Z / naprAB.Z - naprCD.Y не равно 0	


	if (naprAB.Z != 0)
	{
		if (naprAB.X * naprCD.Z / naprAB.Z - naprCD.X != 0)
		{
			double s0 = (CD.start.X - naprAB.X * (CD.start.Z - AB.start.Z) / naprAB.Z - AB.start.X) / (naprAB.X * naprCD.Z / naprAB.Z - naprCD.X);
			
			double x0 = naprCD.X * s0 + CD.start.X;
			double y0 = naprCD.Y * s0 + CD.start.Y;
			double z0 = naprCD.Z * s0 + CD.start.Z;


			Vector3D* P = new Vector3D(x0, y0, z0); //точка пересечения отрезков

			return P;
		}
		
		if (naprAB.Y * naprCD.Z / naprAB.Z - naprCD.Y != 0)
		{
			double s0 = (CD.start.Y - naprAB.Y * (CD.start.Z - AB.start.Z) / naprAB.Z - AB.start.Y) / (naprAB.Y * naprCD.Z / naprAB.Z - naprCD.Y);

			double x0 = naprCD.X * s0 + CD.start.X;
			double y0 = naprCD.Y * s0 + CD.start.Y;
			double z0 = naprCD.Z * s0 + CD.start.Z;


			Vector3D* P = new Vector3D(x0, y0, z0); //точка пересечения отрезков

			return P;
		}

	}



	double x0 = AB.start.X;
	double y0 = AB.start.Y;
	double z0 = AB.start.Z;


	Vector3D* P = new Vector3D (x0,y0,z0); //точка пересечения отрезков
	return P;


}

Vector3D * Intersect(Segment3D AB, Segment3D CD)
{
	Vector3D* P = NULL; //Указатель на точку пересечения отрезков

	Vector3D VectorAB = AB.napr();
	Vector3D VectorCD = CD.napr();
	double k = VectorAB.X / VectorCD.X;
	Vector3D VectorABsmall = VectorAB.DivideOnK(k);
	if (RavenstvoVectorov(VectorABsmall, VectorCD) == true) // проверяем коллинеарны ли или противоположны AB и CD
	{
		cout << "паралельные отрезки" << endl;
		P = NULL;
		return P;

	}
	if (OdnaPloskost(AB, CD) == false) // проверяем лежат ли 4 точки на одной плоскости
	{
		P = NULL;
		return P;
	}

	P = PoiskTochki(AB, CD); // 2 отрезка не парралельны и лежат на одной плоскости, находим точку

	double rAB = sqrt(pow(AB.end.X - AB.start.X, 2) + pow(AB.end.Y - AB.start.Y, 2) + pow(AB.end.Z - AB.start.Z, 2)) / 2; // половина длины отрезка AB
	double rCD = sqrt(pow(CD.end.X - CD.start.X, 2) + pow(CD.end.Y - CD.start.Y, 2) + pow(CD.end.Z - CD.start.Z, 2)) / 2; // половина дляины отрезка CD
	Vector3D centerAB;
	Vector3D centerCD;
	double centerABx = AB.start.X + (AB.end.X - AB.start.X) / 2;
	double centerABy = AB.start.Y + (AB.end.Y - AB.start.Y) / 2;
	double centerABz = AB.start.Z + (AB.end.Z - AB.start.Z) / 2;
	
	double centerCDx = CD.start.X + (CD.end.X - CD.start.X) / 2;
	double centerCDy = CD.start.Y + (CD.end.Y - CD.start.Y) / 2;
	double centerCDz = CD.start.Z + (CD.end.Z - CD.start.Z) / 2;

	centerAB = Vector3D(centerABx, centerABy, centerABz);
	centerCD = Vector3D(centerCDx, centerCDy, centerCDz);
	double rastABtoP = sqrt(pow(P->X - centerAB.X, 2) + pow(P->Y - centerAB.Y, 2) + pow(P->Z - centerAB.Z, 2)); // расстояние от цетра отрезка AB до точки P
	double rastCDtoP = sqrt(pow(P->X - centerCD.X, 2) + pow(P->Y - centerCD.Y, 2) + pow(P->Z - centerCD.Z, 2)); // расстояние от цетра отрезка AB до точки P
	
	//cout << "rAB " << rAB << " rastABtoP " << rastABtoP << endl;
	//cout << "rCD " << rCD << " rastCDtoP " << rastCDtoP << endl;
	//cout << "середина AB: " << centerABx << " " << centerABy << " " << centerABz << endl;
	//cout << "середина CD: " << centerCDx << " " << centerCDy << " " << centerCDz << endl;

	if ((rastABtoP <= rAB) && (rastCDtoP <= rCD))
	{
		return P;
	}
	else
	{
		delete P;
		P = NULL;
		return P;
	}
}


void main()
{
	setlocale(LC_ALL, "Russian");
	Vector3D* Per; //Указатель на точку пересечения отрезков

	double x[4], y[4], z[4];
	cin >> x[0] >> y[0] >> z[0];
	cout << endl;
	cin >> x[1] >> y[1] >> z[1];
	cout << endl;
	cin >> x[2] >> y[2] >> z[2];
	cout << endl;
	cin >> x[3] >> y[3] >> z[3];
	cout << endl;

	Vector3D a (x[0], y[0], z[0]);
	Vector3D b (x[1], y[1], z[1]);
	Vector3D c (x[2], y[2], z[2]);
	Vector3D d (x[3], y[3], z[3]);

	Segment3D ab (a, b);
	Segment3D cd (c, d);

	Per = Intersect(ab, cd);

	cout << "точка пересечения:" << endl;
	if (Per == NULL)
	{
		cout << "точки нету" << endl;
	}

	cout << Per->X << endl;
	cout << Per->Y << endl;
	cout << Per->Z << endl;


	_getch();

	delete Per;
	
}

