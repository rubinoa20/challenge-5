int l_motor = 0; 
int r_motor = 2; 
int range_side = 2;
int range_front = 1;
int f_average = 200;
int s_average = 300;
int forward = 35;
int f_speed = 90;
int s_speed = 90;
int backward = -40;
int speed_r = 60;
int pause = 1000;

void forwards(){
    motor(l_motor,forward);
    motor(r_motor,forward);
    ao();
}
void f_turn(){
    motor(l_motor,f_speed);
    motor(r_motor,forward);
}
void s_turn(){
    motor(l_motor,forward);
    motor(r_motor,s_speed);
}
void turn(){
    motor(l_motor,backward);
    motor(r_motor,speed_r);
    msleep(pause);
    ao();
}
void turn_flip(){
	motor(r_motor,backward);
    motor(l_motor,speed_r);
    msleep(pause);
    ao();
}
void turn_dos(){
    motor(l_motor,speed_r);
    motor(r_motor,10);
    msleep(2000);
    ao();
}
void wall_run(){
    while (analog(range_front) >= f_average){
     	forwards();
    if (analog(range_side) >= s_average){
     	f_turn();
    }
    if (analog(range_side) <= s_average){
        s_turn();
    }
    }
}
void wall_run_dos(){
    while (analog(range_front) >= 600){
     	forwards();
    if (analog(range_side) >= s_average){
     	f_turn();
    }
    if (analog(range_side) <= s_average){
        s_turn();
    }
    }
}

int main()
{
	f_turn();
	msleep(pause);
    printf("Find the wall/n");
    wall_run();
	turn();
	wall_run();
	turn();
	wall_run_dos();
	turn_dos();
	wall_run();
	turn();
	wall_run();
	turn();
	wall_run();
}
