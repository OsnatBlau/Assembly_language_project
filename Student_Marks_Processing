Main,			LDA open_msg_ptr
				BSA puts
				BSA newline
				BSA GetGrades
				BSA FinalOutput
				HLT
				
// General variables		
        student_num,	  DEC 0
        itrval_cnt_ptr,	HEX 500
        ascii_Offset, 	HEX 30			
        const_cr,		    HEX 0D				//'\n'
        const_space,	  HEX 20
        num_arr_ptr,	  HEX 700
        intval_cnt_ptr,	HEX 705
        intval_str_ptr,	HEX 710
        open_msg_ptr,	  HEX 814
        error_msg_ptr,	HEX 800
        intvl_msg_ptr,	HEX 847
        stnd_msg_ptr,	  HEX 83D



//I/O functions
//Function newline
newline,		HEX 0					
				LDA const_cr			
				BSA putc				
				BUN newline I	
//Function Tab
Tab,		  HEX 0					
				LDA const_space			
				BSA putc
				LDA const_space			
				BSA putc	
				LDA const_space			
				BSA putc	
				LDA const_space			
				BSA putc					
				BUN Tab I					
//Function puts
puts,			HEX 0				
				STA putc_TempStr			
Whileps,		LDA putc_TempStr I			
				SZA					
				Bun Print_char			
				Bun puts I			
Print_char,		LDA putc_TempStr I			
				BSA putc					
				ISZ putc_TempStr			
				BUN Whileps	
//Function puts Data
putc_TempStr, 		HEX 0
				
//Function getc
Getc,			HEX 0				
Input_loop_gc,  		SKI				  
				BUN Input_loop_gc			
				INP				
Echogetc,  		SKO				
				BUN Echogetc			
				OUT				
				BUN Getc  I			

//Function Putc
Putc,			HEX 0				
Output_loop_pc, 		SKO					
				BUN Output_loop_pc		
				OUT					
				BUN Putc  I			

//Function PrintInt
PrintInt,			HEX 0				
				STA TempNum_PSI		
				CLA					
				STA leadzero		
				STA tmp_num_toprnt	
				LDA TempNum_PSI		
				LDA Power10ptr_PSI	
				STA ptr_PSI			
				CLA					
				STA FourCounter_PSI	
PSI_for_loop,		LDA It_count_PSI	
				CMA					
				INC					
				ADD FourCounter_PSI	
				SZA					
				BUN PSI_Loop_Body	
				BUN PSI_LoopEnd	
PSI_Loop_Body,		LDA ptr_PSI I		
				STA Divisor		
				CMA					
				INC					
				STA mDivisor	
				CLA					
				STA digit_PSI		
PSI_Loop,			LDA mDivisor	
				ADD TempNum_PSI		
				SNA					
				BUN PSI_Countin		
				BUN PSI_Outdig 		
PSI_Countin, 		LDA mDivisor	
				ADD TempNum_PSI		
				STA TempNum_PSI		  
				ISZ digit_PSI		
				BUN PSI_Loop		
PSI_Outdig,		LDA TempNum_PSI		
				STA Remainder_PSI	
				LDA digit_PSI		
				ADD ascii_Offset	
				STA tmp_num_toprnt	
				LDA digit_PSI		
				SPA					
				BUN PSI_NextZero	
				CLA					
				INC					
				STA leadzero		
PSI_NextZero,		LDA leadzero		
				SPA					
				BUN LeadZeroSkip_psi
				LDA tmp_num_toprnt	
Output_loop2_psi,		SKO					
				BUN Output_loop2_psi
				OUT					
LeadZeroSkip_psi,		ISZ ptr_PSI			
				ISZ FourCounter_PSI	
				BUN PSI_for_loop		
PSI_LoopEnd,		LDA TempNum_PSI		
				ADD ascii_Offset	
Output_loop3_psi,		SKO					
				BUN Output_loop3_psi
				OUT					
				BUN PrintInt I

//Subroutine PrintInt Data
sign_PSI,			      DEC 0			//
TempNum_PSI,		    DEC 0			//
FourCounter_PSI,		DEC 0			//
It_count_PSI,		    DEC 2			// Max loop count
Power10ptr_PSI, 		HEX 750			// @Power10Array
ptr_PSI,			      HEX 0			// 
leadzero,			      HEX 0			//
tmp_num_toprnt,		  HEX 0			//		

// Data Divison
Divisor,			      DEC 0			//
mDivisor,			      DEC 0			//
digit_PSI,			    DEC 0			// result
Remainder_PSI,		  DEC 0			// remainder	

//End of I/O Functions
//**************************************************************************************************//
//Start of Grade Input Functions

//Function GetNum
GetNum,			HEX 0
				STA GN_ptr
				CLA
				STA GN_count
				BSA getc
				STA GN_char
GN_while,			LDA const_cr
				CMA
				INC
				ADD GN_char
				SZA
				BUN GN_notcr
				BUN GN_end_loop
GN_notcr,			LDA GN_count
				ADD GN_maxchar
				SZA
				BUN GN_body
				BUN GN_end_loop
GN_body,			LDA GN_char
				STA GN_ptr I
				ISZ GN_count
				ISZ GN_ptr
				BSA getc
				STA GN_char
				BUN GN_while
GN_end_loop,		CLA
				CLE
				STA GN_ptr I
				STA NumArray_end
				BUN GetNum I
							
				
//Function GetNum Data
        GN_ptr,			  HEX 0
        GN_char,			HEX 0
        GN_count,		  DEC 0
        GN_maxchar,		DEC -5
        const_neg_bs,	DEC -8				//-'BS'



//Function IfDecimal
IfDecimal,			HEX 0
				STA num_to_check
				LDA ascii_Offset
				CMA
				INC
				ADD num_to_check
				STA mASCI
				SNA
				BUN IfUnder10
				BUN CD_false
IfUnder10,		LDA mASCI
				ADD minusTen
				SNA
				BUN CD_false
CD_true,			CLA
				INC
				BUN IfDecimal I
CD_false,			CLA
				BUN IfDecimal I
//Function IfDecimal Data
num_to_check,		DEC 0
mASCI,			DEC 0


//Function ConvertNum
ConvertNum,		HEX 0
				STA CN_ptr		//CN_ptr = number;
				CLA			//
				STA CN_final_number	// num = 0;
				STA CN_OkFlag		// CN_OkFlag=0;
				STA CN_counter		// CN_counter= 0;
				LDA CN_ptr I 		//
				STA CN_temp_char		// cc= *CN_ptr;
				ISZ CN_ptr 		// CN_ptr++;
				ISZ CN_counter		// CN_counter++;
CN_While,		LDA CN_temp_char	
				SZA			//WHILE (cc != ‘\0’){
				BUN CN_BodyLoop	
				BUN CN_EndLoop	
CN_BodyLoop,		LDA CN_temp_char		
				BSA IfDecimal	
				SPA 		
				ISZ CN_OkFlag	
				LDA ascii_Offset	
				CMA		
				INC		
				ADD CN_temp_char	
				STA CCMinus30		
				CLE	
				CLA			
				LDA CN_final_number
				CIL		
				CIL		
				CIL					
				ADD CN_final_number	//
				ADD CN_final_number	//	num * 10;
				ADD CCMinus30		// 
				STA CN_final_number	//	num = num * 10 + (cc - 30H);
				LDA CN_ptr I 		//
				STA CN_temp_char		// 	cc= *CN_ptr;
				ISZ CN_ptr 		// 	CN_ptr++;
				ISZ CN_counter		//	CN_counter++;
				BUN CN_While		//}
CN_EndLoop,		LDA CN_final_number
				SNA				
				BUN CN_CheckUnder101
				ISZ CN_OkFlag
CN_CheckUnder101,	LDA Minus101
				ADD CN_final_number
				SNA
				ISZ CN_OkFlag
				BUN CN_End		
CN_End,			LDA CN_OkFlag		
				SPA					
				BUN CN_numberOK	
				LDA MinusOne
				BUN ConvertNum I
CN_numberOK,		LDA CN_final_number	
				BUN ConvertNum I	
				
//Function ConvertNum Data
CN_final_number,		HEX 0			
CN_ptr,			HEX 0			
CN_temp_char,		HEX 0			
CCMinus30,		HEX 0			
CN_OkFlag,		DEC 0			
CN_counter,		DEC 0			
Minus101,		DEC -101	


//Function GetGrades
GetGrades,		HEX 0
GG_While,		LDA terminator		//While(num_arr_ptr[0] != 'x')
				CMA
				INC
				ADD num_arr_ptr I
				SZA
				BUN GG_LoopBody
				BUN GG_LoopEnd
GG_LoopBody,		LDA arrow
				BSA putc
				LDA num_arr_ptr
				BSA GetNum
				LDA num_arr_ptr
				BSA ConvertNum
				STA GG_FinalGrade
				SNA 
				BUN GG_NumOk
GG_CheckTer,		LDA terminator		
				CMA
				INC
				ADD num_arr_ptr I
				SZA
				BUN GG_ErrorMsg
				BUN GG_LoopEnd
GG_ErrorMsg,		LDA error_msg_ptr
				BSA puts
				BSA newline
				BUN GG_LoopBody
GG_NumOk,		ISZ student_num
				LDA GG_FinalGrade
				BSA AddInterval
				BUN	GG_While
GG_LoopEnd,		BUN	GetGrades I		
				
//Function GetGrades Data
terminator,		HEX 78		//'x'
arrow,			HEX 3E		//'>'
GG_FinalGrade,		DEC 0


//Function AddInterval
AddInterval,		HEX 0
				STA AI_number
				LDA AI_number
				ADD m10
				SNA
				Bun Check20
				ISZ intval0_cnt_arr
				BUN AddInterval I
Check20,			LDA AI_number
				ADD m20
				SNA
				Bun Check30
				ISZ intval1_cnt_arr
				BUN AddInterval I
Check30,			LDA AI_number
				ADD m30
				SNA
				Bun Check40
				ISZ intval2_cnt_arr
				BUN AddInterval I
Check40,			LDA AI_number
				ADD m40
				SNA
				Bun Check50
				ISZ intval3_cnt_arr
				BUN AddInterval I
Check50,			LDA AI_number
				ADD m50
				SNA
				Bun Check60
				ISZ intval4_cnt_arr
				BUN AddInterval I
Check60,			LDA AI_number
				ADD m60
				SNA
				Bun Check70
				ISZ intval5_cnt_arr
				BUN AddInterval I
Check70,			LDA AI_number
				ADD m70
				SNA
				Bun Check80
				ISZ intval6_cnt_arr
				BUN AddInterval I
Check80,			LDA AI_number
				ADD m80
				SNA
				Bun Check90
				ISZ intval7_cnt_arr
				BUN AddInterval I
Check90,			LDA AI_number
				ADD m90
				SNA
				Bun Check100
				ISZ intval8_cnt_arr
				BUN AddInterval I	
Check100,		ISZ intval9_cnt_arr		
				BUN AddInterval I	

//Function AddInterval
AI_number,		DEC 0
m10,			DEC -10
m20,			DEC -20
m30,			DEC -30
m40,			DEC -40
m50,			DEC -50
m60,			DEC -60
m70,			DEC -70
m80,			DEC -80
m90,			DEC -90


//End of Grades Input Related Function
//*****************************************************//
//Final Output Related Functions




// Final Output Functions
//function FinalOutput
FinalOutput,	HEX 0
				CLA
				CLA
				STA fop_counter
				LDA intval_cnt_ptr
				STA tintvl_cnt_ptr
				LDA intval_str_ptr
				STA tintvl_msg_ptr
				LDA stnd_msg_ptr
				BSA puts
				LDA student_num
				BSA PrintInt
				BSA newline
				LDA intvl_msg_ptr
				BSA puts
				BSA newline
FOP_While,		LDA MinusTen
				ADD fop_counter
				SNA
				BUN FOP_EndLoop
FOP_LoopBody,		LDA tintvl_msg_ptr I
				BSA puts
				BSA Tab
				LDA tintvl_cnt_ptr I
				BSA PrintInt
				BSA Tab
				LDA tintvl_cnt_ptr I
				BSA VisualGraph
				BSA newline
				ISZ tintvl_cnt_ptr
				ISZ tintvl_msg_ptr
				ISZ fop_counter
				BUN FOP_While
FOP_EndLoop,		BUN FinalOutput I
				
				
//function FinalOutput Data
tintvl_cnt_ptr,		DEC 0
tintvl_msg_ptr,		DEC 0
fop_counter,		DEC 0
MinusTen,		DEC -10


//Function VisualGraph
VisualGraph,		HEX 0
				STA VG_Output_num
				CLA
				CLE
				LDA pipe_ascii
				BSA putc
				LDA VG_Output_num
				SPA
				BUN VisualGraph I
				LDA VG_Output_num
				ADD MinusOne
				STA VG_Output_num
VG_While,			LDA VG_Output_num
				SPA
				BUN VG_Loop_End
VG_Body,			LDA dash_ascii
				BSA putc
				LDA VG_Output_num
				ADD MinusOne
				STA VG_Output_num
				BUN VG_While
VG_Loop_End,		LDA str_ascii
				BSA putc
				BUN VisualGraph I
				
//Function VisualGraph data
VG_Output_num,		DEC 0
str_ascii,			HEX 2A		//'*'
dash_ascii,		HEX 2D		//'-'
pipe_ascii,		HEX 7C		//'|'
MinusOne,		DEC -1

//Arrays
		ORG 700
NumArray,		HEX 0
				HEX 0
				HEX 0
				HEX 0
NumArray_end,		HEX 0
		ORG 705
intval0_cnt_arr,	HEX 0
intval1_cnt_arr,	HEX 0
intval2_cnt_arr,	HEX 0
intval3_cnt_arr,	HEX 0
intval4_cnt_arr,	HEX 0
intval5_cnt_arr,	HEX 0
intval6_cnt_arr,	HEX 0
intval7_cnt_arr,	HEX 0
intval8_cnt_arr,	HEX 0
intval9_cnt_arr,	HEX 0
		ORG 710
intval_str_arr,		HEX 870
				HEX 87A
				HEX 884
				HEX 88E
				HEX 898
				HEX 8A2
				HEX 8AC
				HEX 8B6
				HEX 8C0
				HEX 8CA
		ORG 750
Power10Array,		DEC 100		// (10 to power of 2)
			DEC 10		// (10 to power of 1)
//Messages section
		ORG 800
str_error,			HEX	45	//'ERROR! wrong input!'	
				HEX	52
				HEX	52
				HEX	4F
				HEX	52
				HEX	21
				HEX	20
				HEX	77
				HEX	72
				HEX	6F	
				HEX	6E
				HEX	67
				HEX	20
				HEX	69	
				HEX	6E
				HEX	70
				HEX	75	
				HEX	74
				HEX	21
				HEX	0		//null = end of string = '\0'

str_opening,	H	EX 49		//"Input Grades(0-100 <Enter> ) 'x' to stop:"
				HEX 6e
				HEX 70
				HEX 75
				HEX 74
				HEX 20
				HEX 47
				HEX 72
				HEX 61
				HEX 64
				HEX 65
				HEX 73
				HEX 28
				HEX 30
				HEX 2d
				HEX 31
				HEX 30
				HEX 30
				HEX 20
				HEX 3c
				HEX 45
				HEX 6e
				HEX 74
				HEX 65
				HEX 72
				HEX 3e
				HEX 20
				HEX 29
				HEX 27
				HEX 78
				HEX 27
				HEX 20
				HEX 74
				HEX 6f
				HEX 20
				HEX 73
				HEX 74
				HEX 6f
				HEX 70
				HEX 3a
				HEX 0		//null = end of string = '\0'
				
str_student,		HEX 53		//'Students:'
				HEX 74
				HEX 75
				HEX 64
				HEX 65
				HEX 6e
				HEX 74
				HEX 73
				HEX 3a
				HEX 0		//null = end of string = '\0'
				
str_interval,		HEX 49		//'Interval:    Freq.'
				HEX 6e
				HEX 74
				HEX 65
				HEX 72
				HEX 76
				HEX 61
				HEX 6c
				HEX 3a
				HEX 20
				HEX 20
				HEX 20
				HEX 46
				HEX 72
				HEX 65
				HEX 71
				HEX 2e
				HEX 0		//null = end of string = '\0'
		ORG 870
str_interva0,	HEX 20		//'   0-9:'
				HEX 20
				HEX 20
				HEX 20
				HEX 20
				HEX 30
				HEX 2d
				HEX 39
				HEX 3a
				HEX 0		//null = end of string = '\0'
str_interva1,	HEX 20		//' 10-19:'
				HEX 20
				HEX 20
				HEX 31		
				HEX 30
				HEX 2d
				HEX 31
				HEX 39
				HEX 3a
				HEX 0		//null = end of string = '\0'
str_interva2,	HEX 20		//' 20-29:'
				HEX 20
				HEX 20
				HEX 32		
				HEX 30
				HEX 2d
				HEX 32
				HEX 39
				HEX 3a
				HEX 0		//null = end of string = '\0'
str_interva3,	HEX 20		//' 30-39:'
				HEX 20
				HEX 20
				HEX 33		
				HEX 30		
				HEX 2d
				HEX 33
				HEX 39
				HEX 3a
				HEX 0		//null = end of string = '\0'
str_interva4,	HEX 20		//' 40-49:'
				HEX 20
				HEX 20
				HEX 34		
				HEX 30
				HEX 2d
				HEX 34
				HEX 39
				HEX 3a
				HEX 0		//null = end of string = '\0'
str_interva5,	HEX 20		//' 50-59:'
				HEX 20
				HEX 20
				HEX 35		
				HEX 30
				HEX 2d
				HEX 35
				HEX 39
				HEX 3a
				HEX 0		//null = end of string = '\0'
str_interva6,	HEX 20		//' 60-69:'
				HEX 20
				HEX 20
				HEX 36		
				HEX 30
				HEX 2d
				HEX 36
				HEX 39
				HEX 3a
				HEX 0		//null = end of string = '\0'
str_interva7,	HEX 20		//' 70-79:'
				HEX 20
				HEX 20
				HEX 37		
				HEX 30
				HEX 2d
				HEX 37
				HEX 39
				HEX 3a
				HEX 0		//null = end of string = '\0'
str_interva8,	HEX 20		//' 80-89:'
				HEX 20
				HEX 20
				HEX 38		
				HEX 30
				HEX 2d
				HEX 38
				HEX 39
				HEX 3a
				HEX 0		//null = end of string = '\0'
str_interva9,	HEX 20		//'90-100:'
				HEX 20
				HEX 39			
				HEX 30
				HEX 2d
				HEX 31
				HEX 30
				HEX 30
				HEX 3a
				HEX 0		//null = end of string = '\0'
