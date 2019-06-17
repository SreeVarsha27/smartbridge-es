#include "lcd_d.h"
void send_a_command(unsigned char command)
{
	
	PORTC=command;
	PORTD&=~(1<<RS);
	PORTD|=(1<<E);
	_delay_ms(50);
	PORTD&=~(1<<E);
	PORTC=0;
}
void send_a_character(unsigned char character)
{
	PORTC=character;
	PORTD|=(1<<RS);
	PORTD|=(1<<E);
	_delay_ms(50);
	PORTD&=~(1<<E);
	PORTC=0;
}


void send_a_string(char*string_of_characters)
{
	
	while(*string_of_characters>0)
	{
		
		send_a_character(*string_of_characters++);
	}
	
}
void LCD_Init(void)
{
	
	DDRC=0XFF;//lcd output

	DDRD=0XFF;//lcd output
	send_a_command(0X01);
	_delay_ms(50);
	send_a_command(0X38);
	_delay_ms(50);

	send_a_command(0X0E);
	_delay_ms(50);

	
}