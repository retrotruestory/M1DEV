#Magic-1 Microcode
<pre>V2.3 by Bill Buzbee.</pre>

<h3>Bottom half of PROM -&nbsp; (starting point of each instruction, using opcode as direct index)</h3>
<table border="1" width="916" height="6345" id="table1" bordercolordark="#003399" bordercolorlight="#003399">

						<tr>

							<td width="33" height="19">0x00</td>
							<td width="235" height="19">halt</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">MISC(M_HALT),DEC_TO_Z(R_PC),L(R_PC,LWORD),CODE,NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x01</td>
							<td width="235" height="19">ld.8 A,#u16_u8_10(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Lda8_16">Lda8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x02</td>
							<td width="235" height="19">push C</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_C),L(R_MDR,LWORD),NEXT(<a href="#Push16">Push16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x03</td>
							<td width="235" height="19">push PC</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_TPC),L(R_MDR,LWORD),NEXT(<a href="#Push16">Push16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x04</td>
							<td width="235" height="19">push DP</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_DP),L(R_MDR,LWORD),NEXT(<a href="#Push16">Push16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x05</td>
							<td width="235" height="19">ld.8 B,#u16_u8_10(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Ldb8_16">Ldb8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x06</td>
							<td width="235" height="19">push A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_MDR,LWORD),NEXT(<a href="#Push16">Push16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x07</td>
							<td width="235" height="19">push B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Push16">Push16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x08</td>
							<td width="235" height="19">br.ne #d16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#BrNegated">BrNegated</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x09</td>
							<td width="235" height="19">pop MSW</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_SP),DATA,NEXT(<a href="#Pop16">Pop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x0a</td>
							<td width="235" height="19">pop C</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_SP),DATA,NEXT(<a href="#Pop16">Pop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x0b</td>
							<td width="235" height="19">pop PC</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_SP),DATA,NEXT(<a href="#Pop16">Pop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x0c</td>
							<td width="235" height="19">pop DP</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_SP),DATA,NEXT(<a href="#Pop16">Pop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x0d</td>
							<td width="235" height="19">pop SP</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_SP),DATA,NEXT(<a href="#Pop16">Pop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x0e</td>
							<td width="235" height="19">pop A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_SP),DATA,NEXT(<a href="#Pop16">Pop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x0f</td>
							<td width="235" height="19">pop B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_SP),DATA,NEXT(<a href="#Pop16">Pop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x10</td>
							<td width="235" height="19">ld.8 A,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Lda8_16">Lda8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x11</td>
							<td width="235" height="19">ld.8 A,#u8(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Lda8_8">Lda8_8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x12</td>
							<td width="235" height="19">ld.8 A,#u16(A)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Lda8_16">Lda8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x13</td>
							<td width="235" height="19">ld.8 A,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Lda8_16">Lda8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x14</td>
							<td width="235" height="19">ld.8 B,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Ldb8_16">Ldb8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x15</td>
							<td width="235" height="19">ld.8 B,#u8(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Ldb8_8">Ldb8_8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x16</td>
							<td width="235" height="19">ld.8 B,#u16(A)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Ldb8_16">Ldb8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x17</td>
							<td width="235" height="19">ld.8 B,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Ldb8_16">Ldb8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x18</td>
							<td width="235" height="19">ld.16 A,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Lda16_16">Lda16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x19</td>
							<td width="235" height="19">ld.16 A,#u16_u8_68(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Lda16_16">Lda16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x1a</td>
							<td width="235" height="19">ld.16 A,#u16(A)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Lda16_16">Lda16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x1b</td>
							<td width="235" height="19">ld.16 A,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Lda16_16">Lda16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x1c</td>
							<td width="235" height="19">ld.16 B,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Ldb16_16">Ldb16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x1d</td>
							<td width="235" height="19">ld.16 B,#u16_u8_68(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Ldb16_16">Ldb16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x1e</td>
							<td width="235" height="19">ld.16 B,#u16(A)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Ldb16_16">Ldb16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x1f</td>
							<td width="235" height="19">ld.16 B,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Ldb16_16">Ldb16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x20</td>
							<td width="235" height="19">sub.8 A,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop8_indir16">Aluop8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x21</td>
							<td width="235" height="19">sub.8 A,#u16(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop8_indir16">Aluop8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x22</td>
							<td width="235" height="19">push MSW</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_MSW),L(R_MDR,LWORD),NEXT(<a href="#Push16">Push16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x23</td>
							<td width="235" height="19">sub.8 A,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop8_indir16">Aluop8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x24</td>
							<td width="235" height="19">sub.8 A,#i8_1</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Aluop8">Aluop8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x25</td>
							<td width="235" height="19">sub.16 (--A),(--B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">DEC_TO_Z(R_A),DATA,NEXT(<a href="#Mop16">Mop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x26</td>
							<td width="235" height="19">push SP</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_SP),L(R_MDR,LWORD),NEXT(<a href="#Push16">Push16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x27</td>
							<td width="235" height="19">sub.8 A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Aluop8">Aluop8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x28</td>
							<td width="235" height="19">sub.16 A,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_indir16">Aluop16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x29</td>
							<td width="235" height="19">sub.16 A,#u16(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_indir16">Aluop16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x2a</td>
							<td width="235" height="19">sbc.16 (--A),(--B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">DEC_TO_Z(R_A),DATA,NEXT(<a href="#Mop16Carry">Mop16Carry</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x2b</td>
							<td width="235" height="19">sub.16 A,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_indir16">Aluop16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x2c</td>
							<td width="235" height="19">sub.16 A,#i16_exti8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_16">Aluop16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x2d</td>
							<td width="235" height="19">sub.16 A,#exti8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMEXT,NEXT(<a href="#Aluop16">Aluop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x2e</td>
							<td width="235" height="19">wcpte A,(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">PRIV(1),TO_Z(R_B),SET_ADR(CODE_SPACE,PTB_OVERRIDE),NEXT(<a href="#Wcpte">Wcpte</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x2f</td>
							<td width="235" height="19">sub.16 A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Aluop16">Aluop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x30</td>
							<td width="235" height="19">add.8 A,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop8_indir16">Aluop8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x31</td>
							<td width="235" height="19">add.8 A,#u16(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop8_indir16">Aluop8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x32</td>
							<td width="235" height="19">br A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_PC,LWORD),CODE,NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x33</td>
							<td width="235" height="19">add.8 A,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop8_indir16">Aluop8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x34</td>
							<td width="235" height="19">add.8 A,#i8_1</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Aluop8">Aluop8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x35</td>
							<td width="235" height="19">add.16 (--A),(--B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">DEC_TO_Z(R_A),DATA,NEXT(<a href="#Mop16">Mop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x36</td>
							<td width="235" height="19">add.8 A,A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_MDR,LWORD),NEXT(<a href="#Aluop8">Aluop8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x37</td>
							<td width="235" height="19">add.8 A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Aluop8">Aluop8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x38</td>
							<td width="235" height="19">add.16 A,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_indir16">Aluop16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x39</td>
							<td width="235" height="19">add.16 A,#u16(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_indir16">Aluop16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x3a</td>
							<td width="235" height="19">syscall #sys_num8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Syscall">Syscall</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x3b</td>
							<td width="235" height="19">add.16 A,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_indir16">Aluop16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x3c</td>
							<td width="235" height="19">add.16 A,#i16_exti8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_16">Aluop16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x3d</td>
							<td width="235" height="19">add.16 A,#exti8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMEXT,NEXT(<a href="#Aluop16">Aluop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x3e</td>
							<td width="235" height="19">add.16 A,A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_MDR,LWORD),NEXT(<a href="#Aluop16">Aluop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x3f</td>
							<td width="235" height="19">add.16 A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Aluop16">Aluop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x40</td>
							<td width="235" height="19">cmp.8 A,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmp8_indir16">Cmp8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x41</td>
							<td width="235" height="19">cmp.8 A,#u16(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmp8_indir16">Cmp8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x42</td>
							<td width="235" height="19">copy C,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_C,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x43</td>
							<td width="235" height="19">cmp.8 A,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmp8_indir16">Cmp8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x44</td>
							<td width="235" height="19">cmp.8 A,#i8_0</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Cmp8">Cmp8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x45</td>
							<td width="235" height="19">cmp.8 A,#0</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_SUB,BYTE,NO_CARRY),MISC(M_SET_FLAGS),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x46</td>
							<td width="235" height="19">xor.16 A,A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_MDR,LWORD),NEXT(<a href="#Aluop16">Aluop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x47</td>
							<td width="235" height="19">cmp.8 A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Cmp8">Cmp8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x48</td>
							<td width="235" height="19">cmp.16 A,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmp16_indir16">Cmp16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x49</td>
							<td width="235" height="19">cmp.16 A,#u16(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmp16_indir16">Cmp16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x4a</td>
							<td width="235" height="19">sh0add B,A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_MDR,LWORD),NEXT(<a href="#LeaB1">LeaB1</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x4b</td>
							<td width="235" height="19">cmp.16 A,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmp16_indir16">Cmp16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x4c</td>
							<td width="235" height="19">cmp.16 A,#i16_exti8_0</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmp16_16">Cmp16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x4d</td>
							<td width="235" height="19">cmp.16 A,#exti8_0</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMEXT,NEXT(<a href="#Cmp16">Cmp16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x4e</td>
							<td width="235" height="19">cmp.16 A,#0</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_SUB,WORD,NO_CARRY),MISC(M_SET_FLAGS),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x4f</td>
							<td width="235" height="19">cmp.16 A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Cmp16">Cmp16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x50</td>
							<td width="235" height="19">or.8 A,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop8_indir16">Aluop8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x51</td>
							<td width="235" height="19">or.8 A,#u16(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop8_indir16">Aluop8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x52</td>
							<td width="235" height="19">sex A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z8(R_A),L(R_A,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x53</td>
							<td width="235" height="19">or.8 A,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop8_indir16">Aluop8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x54</td>
							<td width="235" height="19">or.8 A,#i8_1</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Aluop8">Aluop8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x55</td>

							<td width="235" height="19">or.16 (--A),(--B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">DEC_TO_Z(R_A),DATA,NEXT(<a href="#Mop16">Mop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x56</td>
							<td width="235" height="19">br.leu #d16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#BrNormal">BrNormal</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x57</td>
							<td width="235" height="19">or.8 A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Aluop8">Aluop8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x58</td>
							<td width="235" height="19">or.16 A,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_indir16">Aluop16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x59</td>
							<td width="235" height="19">or.16 A,#u16(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_indir16">Aluop16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x5a</td>
							<td width="235" height="19">sh1add A,B,A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_MDR,LWORD),NEXT(<a href="#LeaABA2">LeaABA2</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x5b</td>
							<td width="235" height="19">or.16 A,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_indir16">Aluop16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x5c</td>
							<td width="235" height="19">or.16 A,#i16_exti8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_16">Aluop16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x5d</td>
							<td width="235" height="19">or.16 A,#exti8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMEXT,NEXT(<a href="#Aluop16">Aluop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x5e</td>
							<td width="235" height="19">br.gtu #d16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#BrNegated">BrNegated</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x5f</td>
							<td width="235" height="19">or.16 A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Aluop16">Aluop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x60</td>
							<td width="235" height="19">and.8 A,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop8_indir16">Aluop8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x61</td>
							<td width="235" height="19">and.8 A,#u16(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop8_indir16">Aluop8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x62</td>
							<td width="235" height="19">sh1add B,A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#LeaBAB2">LeaBAB2</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x63</td>
							<td width="235" height="19">and.8 A,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop8_indir16">Aluop8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x64</td>
							<td width="235" height="19">and.8 A,#i8_1</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Aluop8">Aluop8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x65</td>
							<td width="235" height="19">and.16 (--A),(--B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">DEC_TO_Z(R_A),DATA,NEXT(<a href="#Mop16">Mop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x66</td>
							<td width="235" height="19">nop</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x67</td>
							<td width="235" height="19">and.8 A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Aluop8">Aluop8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x68</td>
							<td width="235" height="19">and.16 A,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_indir16">Aluop16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x69</td>
							<td width="235" height="19">and.16 A,#u16(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_indir16">Aluop16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x6a</td>
							<td width="235" height="19">sh1add B,B,A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_MDR,LWORD),NEXT(<a href="#LeaBBA2">LeaBBA2</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x6b</td>
							<td width="235" height="19">and.16 A,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_indir16">Aluop16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x6c</td>
							<td width="235" height="19">and.16 A,#i16_exti8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Aluop16_16">Aluop16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x6d</td>
							<td width="235" height="19">and.16 A,#exti8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMEXT,NEXT(<a href="#Aluop16">Aluop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x6e</td>
							<td width="235" height="19">strcopy</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),DATA,NEXT(<a href="#Strcopy">Strcopy</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x6f</td>
							<td width="235" height="19">and.16 A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Aluop16">Aluop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x70</td>
							<td width="235" height="19">lea A,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#LdaA_16">LdaA_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x71</td>
							<td width="235" height="19">lea A,#u16(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#LdaA_16">LdaA_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x72</td>
							<td width="235" height="19">lea A,#u16(A)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#LdaA_16">LdaA_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x73</td>
							<td width="235" height="19">lea A,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#LdaA_16">LdaA_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x74</td>
							<td width="235" height="19">lea B,#u16(DP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#LdaB_16">LdaB_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x75</td>
							<td width="235" height="19">lea B,#u16(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#LdaB_16">LdaB_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x76</td>
							<td width="235" height="19">lea B,#u16(A)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#LdaB_16">LdaB_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x77</td>
							<td width="235" height="19">lea B,#u16(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#LdaB_16">LdaB_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x78</td>
							<td width="235" height="19">ld.8 A,#u8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#LdiA8">LdiA8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x79</td>
							<td width="235" height="19">ld.8 B,#u8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#LdiB8">LdiB8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x7a</td>
							<td width="235" height="19">ld.16 A,#exti8_u16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMEXT,NEXT(<a href="#LdiA16">LdiA16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x7b</td>
							<td width="235" height="19">ld.16 B,#exti8_u16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMEXT,NEXT(<a href="#LdiB16">LdiB16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x7c</td>
							<td width="235" height="19">ld.16 A,#u16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#LdiA16_lo">LdiA16_lo</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x7d</td>
							<td width="235" height="19">ld.16 B,#u16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#LdiB16_lo">LdiB16_lo</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x7e</td>
							<td width="235" height="19">adc.16 A,A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_MDR,LWORD),NEXT(<a href="#Adc16">Adc16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x7f</td>
							<td width="235" height="19">adc.16 A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Adc16">Adc16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x80</td>
							<td width="235" height="19">call #d16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#CallImm">CallImm</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x81</td>
							<td width="235" height="19">ld.16 A,#u8(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Lda16_8">Lda16_8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x82</td>
							<td width="235" height="19">call A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_PC),L(R_MDR,LWORD),NEXT(<a href="#CallA">CallA</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x83</td>
							<td width="235" height="19">br #d16_d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#RelBrLo">RelBrLo</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x84</td>
							<td width="235" height="19">sbr #d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMEXT,NEXT(<a href="#RelBr">RelBr</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x85</td>
							<td width="235" height="19">ld.16 B,#u8(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Ldb16_8">Ldb16_8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x86</td>
							<td width="235" height="19">lea A,#u8(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#LeaShort">LeaShort</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x87</td>
							<td width="235" height="19">lea B,#u8(SP)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#LeaShort">LeaShort</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x88</td>
							<td width="235" height="19">copy A,MSW</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_MSW),L(R_A,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x89</td>
							<td width="235" height="19">br.eq #d16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#BrNormal">BrNormal</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x8a</td>
							<td width="235" height="19">reti</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">PRIV(1),NEXT(<a href="#Reti">Reti</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x8b</td>
							<td width="235" height="19">trapo</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">MISC(M_TRAPO),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x8c</td>
							<td width="235" height="19">bset.8 A,#mask8,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Bset8">Bset8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x8d</td>
							<td width="235" height="19">bclr.8 A,#mask8,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Bclr8">Bclr8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x8e</td>
							<td width="235" height="19">bset.16 A,#mask16,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Bset16">Bset16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x8f</td>
							<td width="235" height="19">bclr.16 A,#mask16,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Bclr16">Bclr16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x90</td>
							<td width="235" height="19">cmpb.eq.8 A,#u16(DP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb8_indir16">Cmpb8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x91</td>
							<td width="235" height="19">cmpb.eq.8 A,#u16(SP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb8_indir16">Cmpb8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x92</td>
							<td width="235" height="19">copy B,A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_B,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x93</td>
							<td width="235" height="19">cmpb.eq.8 A,#u16(B),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb8_indir16">Cmpb8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x94</td>
							<td width="235" height="19">cmpb.eq.8 A,#i8_0,#d8</td>
							<td width="10" height="13">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Cmpb8">Cmpb8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x95</td>
							<td width="235" height="19">cmpb.eq.8 A,#0,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_MDR),L(R_MDR,LWORD),NEXT(<a href="#Cmpb8">Cmpb8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x96</td>
							<td width="235" height="19">copy C,A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_C,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x97</td>
							<td width="235" height="19">cmpb.eq.8 A,B,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Cmpb8">Cmpb8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x98</td>
							<td width="235" height="19">cmpb.eq.16 A,#u16(DP),#d8</td>
							<td width="10" height="13">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_indir16">Cmpb16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x99</td>
							<td width="235" height="19">cmpb.eq.16 A,#u16(SP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_indir16">Cmpb16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x9a</td>
							<td width="235" height="19">copy A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_A,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x9b</td>
							<td width="235" height="19">cmpb.eq.16 A,#u16(B),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_indir16">Cmpb16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="13">0x9c</td>
							<td width="235" height="19">cmpb.eq.16 A,#i16_exti8_0,#d8</td>
							<td width="10" height="13">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_16">Cmpb16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x9d</td>
							<td width="235" height="19">cmpb.eq.16 A,#exti8_0,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMEXT,NEXT(<a href="#Cmpb16">Cmpb16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x9e</td>
							<td width="235" height="19">cmpb.eq.16 A,#0,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_MDR),L(R_MDR,LWORD),NEXT(<a href="#Cmpb16">Cmpb16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0x9f</td>
							<td width="235" height="19">cmpb.eq.16 A,B,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Cmpb16">Cmpb16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xa0</td>
							<td width="235" height="19">cmpb.lt.8 A,#u16(DP),#d8</td>
							<td width="10" height="13">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb8_indir16">Cmpb8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xa1</td>
							<td width="235" height="19">cmpb.lt.8 A,#u16(SP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb8_indir16">Cmpb8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xa2</td>
							<td width="235" height="19">sh0add A,A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#LeaA1">LeaA1</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xa3</td>
							<td width="235" height="19">cmpb.lt.8 A,#u16(B),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb8_indir16">Cmpb8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xa4</td>
							<td width="235" height="19">cmpb.lt.8 A,#i8_0,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Cmpb8">Cmpb8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xa5</td>
							<td width="235" height="19">cmpb.lt.8 A,#0,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_MDR),L(R_MDR,LWORD),NEXT(<a href="#Cmpb8">Cmpb8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xa6</td>
							<td width="235" height="19">br.lt #d16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#BrNormal">BrNormal</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xa7</td>
							<td width="235" height="19">cmpb.lt.8 A,B,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Cmpb8">Cmpb8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xa8</td>
							<td width="235" height="19">cmpb.lt.16 A,#u16(DP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_indir16">Cmpb16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xa9</td>
							<td width="235" height="19">cmpb.lt.16 A,#u16(SP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_indir16">Cmpb16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xaa</td>
							<td width="235" height="19">sh1add A,A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#LeaAAB2">LeaAAB2</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xab</td>
							<td width="235" height="19">cmpb.lt.16 A,#u16(B),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_indir16">Cmpb16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xac</td>
							<td width="235" height="19">cmpb.lt.16 A,#i16_exti8,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_16">Cmpb16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xad</td>
							<td width="235" height="19">cmpb.lt.16 A,#exti8,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMEXT,NEXT(<a href="#Cmpb16">Cmpb16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xae</td>
							<td width="235" height="19">br.ge #d16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#BrNegated">BrNegated</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xaf</td>
							<td width="235" height="19">cmpb.lt.16 A,B,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Cmpb16">Cmpb16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xb0</td>
							<td width="235" height="19">cmpb.le.8 A,#u16(DP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb8_indir16">Cmpb8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xb1</td>
							<td width="235" height="19">cmpb.le.8 A,#u16(SP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb8_indir16">Cmpb8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xb2</td>
							<td width="235" height="19">sex B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z8(R_B),L(R_B,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xb3</td>
							<td width="235" height="19">cmpb.le.8 A,#u16(B),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb8_indir16">Cmpb8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xb4</td>
							<td width="235" height="19">cmpb.le.8 A,#i8,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Cmpb8">Cmpb8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xb5</td>
							<td width="235" height="19">br.le #d16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#BrNormal">BrNormal</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xb6</td>
							<td width="235" height="19">copy DP,A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_DP,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xb7</td>
							<td width="235" height="19">cmpb.le.8 A,B,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Cmpb8">Cmpb8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xb8</td>
							<td width="235" height="19">cmpb.le.16 A,#u16(DP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_indir16">Cmpb16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xb9</td>
							<td width="235" height="19">cmpb.le.16 A,#u16(SP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_indir16">Cmpb16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xba</td>
							<td width="235" height="19">adc.16 (--A),(--B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">DEC_TO_Z(R_A),DATA,NEXT(<a href="#Mop16Carry">Mop16Carry</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xbb</td>
							<td width="235" height="19">cmpb.le.16 A,#u16(B),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_indir16">Cmpb16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xbc</td>
							<td width="235" height="19">cmpb.le.16 A,#i16_exti8,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_16">Cmpb16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xbd</td>
							<td width="235" height="19">cmpb.le.16 A,#exti8,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMEXT,NEXT(<a href="#Cmpb16">Cmpb16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xbe</td>
							<td width="235" height="19">br.gt #d16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#BrNegated">BrNegated</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xbf</td>
							<td width="235" height="19">cmpb.le.16 A,B,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Cmpb16">Cmpb16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xc0</td>
							<td width="235" height="19">br.geu #d16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#BrNegated">BrNegated</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xc1</td>
							<td width="235" height="19">st.8 #u16_u8_10(SP),A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Sta8_16">Sta8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xc2</td>
							<td width="235" height="19">shl.16 A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_MDR,LWORD),NEXT(<a href="#Shlb16">Shla16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xc3</td>
							<td width="235" height="19">shr.16 A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),MISC(M_RSHIFT),L(R_A,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xc4</td>
							<td width="235" height="19">shl.16 B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Shlb16">Shlb16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xc5</td>
							<td width="235" height="19">st.8 #u16_u8_10(SP),B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Stb8_16">Stb8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xc6</td>
							<td width="235" height="19">shr.16 B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),MISC(M_RSHIFT),L(R_B,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xc7</td>
							<td width="235" height="19">xor.16 A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Aluop16">Aluop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="1">0xc8</td>
							<td width="235" height="19">copy PTB,A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">PRIV(1),TO_Z(R_A),L(R_PTB,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xc9</td>
							<td width="235" height="19">st.16 #u16_u8_10(SP),A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Sta16_16">Sta16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xca</td>
							<td width="235" height="19">copy MSW,A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">PRIV(1),NEXT(<a href="#CopyMSWA">CopyMSWA</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xcb</td>
							<td width="235" height="19">copy SP,A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_SP,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xcc</td>
							<td width="235" height="19">xor.16 (--A),(--B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">DEC_TO_Z(R_A),DATA,NEXT(<a href="#Mop16">Mop16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xcd</td>
							<td width="235" height="19">st.16 #u16_u8_10(SP),B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Stb16_16">Stb16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xce</td>
							<td width="235" height="19">ld.16  C,#u16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#LdiC16_lo">LdiC16_lo</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xcf</td>
							<td width="235" height="19">br.ltu #d16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#BrNormal">BrNormal</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xd0</td>
							<td width="235" height="19">st.8 #u16(DP),A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Sta8_16">Sta8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xd1</td>
							<td width="235" height="19">st.8  #u8(SP),A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Sta8_8">Sta8_8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xd2</td>
							<td width="235" height="19">st.8  #u16(A),A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Sta8_16">Sta8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xd3</td>
							<td width="235" height="19">st.8  #u16(B),A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Sta8_16">Sta8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xd4</td>
							<td width="235" height="19">st.8  #u16(DP),B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Stb8_16">Stb8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xd5</td>
							<td width="235" height="19">st.8  #u8(SP),B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Stb8_8">Stb8_8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xd6</td>
							<td width="235" height="19">st.8  #u16(A),B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Stb8_16">Stb8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xd7</td>
							<td width="235" height="19">st.8 #u16(B),B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Stb8_16">Stb8_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xd8</td>
							<td width="235" height="19">st.16  #u16(DP),A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Sta16_16">Sta16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xd9</td>
							<td width="235" height="19">st.16 #u8(SP),A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Sta16_8">Sta16_8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xda</td>
							<td width="235" height="19">st.16 #u16(A),A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Sta16_16">Sta16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xdb</td>
							<td width="235" height="19">st.16 #u16(B),A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Sta16_16">Sta16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xdc</td>
							<td width="235" height="19">st.16 #u16(DP),B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Stb16_16">Stb16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xdd</td>
							<td width="235" height="19">st.16 #u8(SP),B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Stb16_8">Stb16_8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xde</td>
							<td width="235" height="19">st.16 #u16(A),B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Stb16_16">Stb16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xdf</td>
							<td width="235" height="19">st.16 #u16(B),B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Stb16_16">Stb16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xe0</td>
							<td width="235" height="19">ldcode.8 A,(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),CODE,NEXT(<a href="#Ldcode8">Ldcode8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xe1</td>
							<td width="235" height="19">copy A,DP</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_DP),L(R_A,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xe2</td>
							<td width="235" height="19">ld.16 C,#exti8_u16</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMEXT,NEXT(<a href="#LdiC16">LdiC16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xe3</td>
							<td width="235" height="19">memcopy4</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">INC2_TO_Z(R_B),DATA,NEXT(<a href="#Mcpy4">Mcpy4</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xe4</td>
							<td width="235" height="19">enter #fsize16_8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Enter">Enter</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xe5</td>
							<td width="235" height="19">enter #fsize8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">NEG1_TO_Z,LATCH(R_MDR),NEXT(<a href="#Enter">Enter</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xe6</td>
							<td width="235" height="19">vshl.16 A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_MDR,LWORD),NEXT(<a href="#Vshl">Vshl</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xe7</td>
							<td width="235" height="19">vshl.16 B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Vshl">Vshl</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xe8</td>
							<td width="235" height="19">memcopy</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">COMPARE_0(R_C),MISC(M_SET_FLAGS),NEXT(<a href="#Bcopy">Bcopy</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xe9</td>
							<td width="235" height="19">tosys</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">PRIV(1),COMPARE_0(R_C),MISC(M_SET_FLAGS),NEXT(<a href="#ToSys">ToSys</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xea</td>
							<td width="235" height="19">fromsys</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">PRIV(1),COMPARE_0(R_C),MISC(M_SET_FLAGS),NEXT(<a href="#FromSys">FromSys</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xeb</td>
							<td width="235" height="19">ldclr.8 A,(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),DATA,NEXT(<a href="#LdClr">LdClr</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xec</td>
							<td width="235" height="19">wdpte A,(B)</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">PRIV(1),TO_Z(R_B),SET_ADR(DATA_SPACE,PTB_OVERRIDE),NEXT(<a href="#Wdpte">Wdpte</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xed</td>
							<td width="235" height="19">sbc.16 A,B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Sbc16">Sbc16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xee</td>
							<td width="235" height="19">vshr.16 A</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_A),L(R_MDR,LWORD),NEXT(<a href="#Vshr">Vshr</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xef</td>
							<td width="235" height="19">vshr.16 B</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Vshr">Vshr</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xf0</td>
							<td width="235" height="19">cmpb.ne.8 A,#u16(DP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb8_indir16">Cmpb8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xf1</td>
							<td width="235" height="19">cmpb.ne.8 A,#u16(SP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb8_indir16">Cmpb8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xf2</td>
							<td width="235" height="19">copy A,C</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_C),L(R_A,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xf3</td>
							<td width="235" height="19">cmpb.ne.8 A,#u16(B),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb8_indir16">Cmpb8_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xf4</td>
							<td width="235" height="19">cmpb.ne.8 A,#i8_0,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMLO,NEXT(<a href="#Cmpb8">Cmpb8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xf5</td>
							<td width="235" height="19">cmpb.ne.8 A,#0,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_MDR),L(R_MDR,LWORD),NEXT(<a href="#Cmpb8">Cmpb8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xf6</td>
							<td width="235" height="19">copy A,SP</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_SP),L(R_A,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xf7</td>
							<td width="235" height="19">cmpb.ne.8 A,B,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Cmpb8">Cmpb8</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xf8</td>
							<td width="235" height="19">cmpb.ne.16 A,#u16(DP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_indir16">Cmpb16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xf9</td>
							<td width="235" height="19">cmpb.ne.16 A,#u16(SP),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_indir16">Cmpb16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xfa</td>
							<td width="235" height="19">bkpt</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">MISC(M_BKPT),NEXT(<a href="#Unreachable">Unreachable</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xfb</td>
							<td width="235" height="19">cmpb.ne.16 A,#u16(B),#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_indir16">Cmpb16_indir16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xfc</td>
							<td width="235" height="19">cmpb.ne.16 A,#i16_exti8_0,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMHI,NEXT(<a href="#Cmpb16_16">Cmpb16_16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xfd</td>
							<td width="235" height="19">cmpb.ne.16 A,#exti8_0,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">LDIMMEXT,NEXT(<a href="#Cmpb16">Cmpb16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xfe</td>
							<td width="235" height="19">cmpb.ne.16 A,#0,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_MDR),L(R_MDR,LWORD),NEXT(<a href="#Cmpb16">Cmpb16</a>)</td>

						</tr>

						<tr>

							<td width="33" height="19">0xff</td>
							<td width="235" height="19">cmpb.ne.16 A,B,#d8</td>
							<td width="10" height="19">;</td>
							<td width="610" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Cmpb16">Cmpb16</a>)</td>

						</tr>

					</table>

						<h4>Top half of PROM - continuation microcode.</h4>

    <table border="1" width="965" height="6380" id="table2" bordercolordark="#003399" bordercolorlight="#003399">

						<tr>

							<td width="41" height="19">0x100</td>
							<td width="122" height="19"><a name="Fetch">Fetch</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">FETCH_OP</td>

						</tr>

						<tr>

							<td width="41" height="19">0x101</td>
							<td width="122" height="19"><a name="IRQ5">IRQ5</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MAR),MISC(M_COMMIT),NEXT(<a href="#Fault">Fault</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x102</td>
							<td width="122" height="19"><a name="IRQ4">IRQ4</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MAR),MISC(M_COMMIT),NEXT(<a href="#Fault">Fault</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x103</td>
							<td width="122" height="19"><a name="IRQ3">IRQ3</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MAR),MISC(M_COMMIT),NEXT(<a href="#Fault">Fault</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x104</td>
							<td width="122" height="19"><a name="IRQ2">IRQ2</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MAR),MISC(M_COMMIT),NEXT(<a href="#Fault">Fault</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x105</td>
							<td width="122" height="19"><a name="IRQ1">IRQ1</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MAR),MISC(M_COMMIT),NEXT(<a href="#Fault">Fault</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x106</td>
							<td width="122" height="19"><a name="IRQ0">IRQ0</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MAR),MISC(M_COMMIT),NEXT(<a href="#Fault">Fault</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x107</td>
							<td width="122" height="19"><a name="DMA_req">DMA_req</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">MISC(M_DMA_ACK),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x108</td>
							<td width="122" height="19"><a name="Fault_syscall">Fault_syscall</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MAR),MISC(M_COMMIT),NEXT(<a href="#Fault">Fault</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x109</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19"></td>

						</tr>

						<tr>

							<td width="41" height="19">0x10a</td>
							<td width="122" height="19"><a name="Fault_ovflo">Fault_ovflo</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MAR),L(R_PC,LWORD),NEXT(<a href="#Fault">Fault</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x10b</td>
							<td width="122" height="19"><a name="Fault_priv">Fault_priv</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MAR),L(R_PC,LWORD),NEXT(<a href="#Fault">Fault</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x10c</td>
							<td width="122" height="19"><a name="Fault_bkpt">Fault_bkpt</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MAR),L(R_PC,LWORD),NEXT(<a href="#Fault">Fault</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x10d</td>
							<td width="122" height="19"><a name="Fault_nw">Fault_nw</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MAR),L(R_PC,LWORD),NEXT(<a href="#Fault">Fault</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x10e</td>
							<td width="122" height="19"><a name="Fault_np">Fault_np</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MAR),L(R_PC,LWORD),NEXT(<a href="#Fault">Fault</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x10f</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19"></td>

						</tr>

						<tr>

							<td width="41" height="19">0x110</td>
							<td width="122" height="19"><a name="Aluop8_indir">Aluop8_indir</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x111</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x112</td>
							<td width="122" height="19"><a name="Aluop8">Aluop8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_IR13,BYTE,NO_CARRY),L(R_A,LBYTE),MISC(M_SET_FLAGS),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x113</td>
							<td width="122" height="19"><a name="Aluop8_indir16">Aluop8_indir16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Aluop8_indir">Aluop8_indir</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x114</td>
							<td width="122" height="19"><a name="Aluop16_indir">Aluop16_indir</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x115</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x116</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x117</td>
							<td width="122" height="19"><a name="Aluop16">Aluop16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_IR13,WORD,NO_CARRY),L(R_A,LWORD),MISC(M_SET_FLAGS),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x118</td>
							<td width="122" height="19"><a name="Aluop16_indir16">Aluop16_indir16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Aluop16_indir">Aluop16_indir</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x119</td>
							<td width="122" height="19"><a name="Cmp8_indir">Cmp8_indir</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x11a</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x11b</td>
							<td width="122" height="19"><a name="Cmp8">Cmp8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_SUB,BYTE,NO_CARRY),MISC(M_SET_FLAGS),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x11c</td>
							<td width="122" height="19"><a name="Cmp8_indir16">Cmp8_indir16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Cmp8_indir">Cmp8_indir</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x11d</td>
							<td width="122" height="19"><a name="Cmp16_indir">Cmp16_indir</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x11e</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x11f</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x120</td>
							<td width="122" height="19"><a name="Cmp16">Cmp16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_SUB,WORD,NO_CARRY),MISC(M_SET_FLAGS),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x121</td>
							<td width="122" height="19"><a name="Cmp16_indir16">Cmp16_indir16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Cmp16_indir">Cmp16_indir</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x122</td>
							<td width="122" height="19"><a name="Cmpb8_indir">Cmpb8_indir</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x123</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x124</td>
							<td width="122" height="19"><a name="Cmpb8">Cmpb8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_SUB,BYTE,NO_CARRY),MISC(M_SET_FLAGS),NEXT(<a href="#CheckBr">CheckBr</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x125</td>
							<td width="122" height="19"><a name="Cmpb8_indir16">Cmpb8_indir16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Cmpb8_indir">Cmpb8_indir</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x126</td>
							<td width="122" height="19"><a name="Cmpb16_indir">Cmpb16_indir</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x127</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x128</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x129</td>
							<td width="122" height="19"><a name="Cmpb16">Cmpb16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_SUB,WORD,NO_CARRY),MISC(M_SET_FLAGS),NEXT(<a href="#CheckBr">CheckBr</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x12a</td>
							<td width="122" height="19"><a name="Cmpb16_indir16">Cmpb16_indir16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Cmpb16_indir">Cmpb16_indir</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x12b</td>
							<td width="122" height="19"><a name="CheckBr">CheckBr</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMEXT,CBR(B_NORMAL,<a href="#TakenBr">TakenBr</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x12c</td>
							<td width="122" height="19"><a name="TakenBr">TakenBr</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_PC),E_R(ER_MDR),ALU(OP_ADD,WORD,NO_CARRY),L(R_PC,LWORD),CODE,NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x12d</td>
							<td width="122" height="19"><a name="BrNormal">BrNormal</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,CBR(B_NORMAL,<a href="#TakenBr">TakenBr</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x12e</td>
							<td width="122" height="19"><a name="BrNegated">BrNegated</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,CBR(B_NEGATED,<a href="#TakenBr">TakenBr</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x12f</td>
							<td width="122" height="19"><a name="Bset8">Bset8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_AND,BYTE,NO_CARRY),MISC(M_SET_FLAGS),NEXT(<a href="#CheckBrNeg">CheckBrNeg</a>)</td>

						</tr>

						<tr>

							<td width="41" height="13">0x130</td>
							<td width="122" height="19"><a name="CheckBrNeg">CheckBrNeg</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMEXT,CBR(B_NEGATED,<a href="#TakenBr">TakenBr</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x131</td>
							<td width="122" height="19"><a name="Bclr8">Bclr8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_AND,BYTE,NO_CARRY),MISC(M_SET_FLAGS),NEXT(<a href="#CheckBr">CheckBr</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x132</td>
							<td width="122" height="19"><a name="Bset16">Bset16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x133</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_AND,WORD,NO_CARRY),MISC(M_SET_FLAGS),NEXT(<a href="#CheckBrNeg">CheckBrNeg</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x134</td>
							<td width="122" height="19"><a name="Bclr16">Bclr16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x135</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_AND,WORD,NO_CARRY),MISC(M_SET_FLAGS),NEXT(<a href="#CheckBr">CheckBr</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x136</td>
							<td width="122" height="19"><a name="Push16">Push16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">DEC_TO_Z(R_SP),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x137</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITELO,DEC_TO_Z(R_MAR),DATA,L(R_SP,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x138</td>
							<td width="122" height="19"><a name="Whi">Whi</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITEHI,TO_Z(R_PC),CODE,NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x139</td>
							<td width="122" height="19"><a name="Pop16">Pop16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x13a</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READLO,INC_TO_Z(R_MAR),L(R_SP,LWORD),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x13b</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MDR),L(R_IR_REG,LWORD),NEXT(<a href="#PCtoMAR">PCtoMAR</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x13c</td>
							<td width="122" height="19"><a name="Lda8_8">Lda8_8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x13d</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDLO,NEXT(<a href="#LdiA8">LdiA8</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x13e</td>
							<td width="122" height="19"><a name="Lda8_16">Lda8_16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Lda8_8">Lda8_8</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x13f</td>
							<td width="122" height="19"><a name="Ldb8_8">Ldb8_8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x140</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDLO,NEXT(<a href="#LdiB8">LdiB8</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x141</td>
							<td width="122" height="19"><a name="Ldb8_16">Ldb8_16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Ldb8_8">Ldb8_8</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x142</td>
							<td width="122" height="19"><a name="Lda16_8">Lda16_8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x143</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x144</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDLO,NEXT(<a href="#LdiA16">LdiA16</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x145</td>
							<td width="122" height="19"><a name="Lda16_16">Lda16_16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Lda16_8">Lda16_8</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x146</td>
							<td width="122" height="19"><a name="Ldb16_8">Ldb16_8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x147</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x148</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDLO,NEXT(<a href="#LdiB16">LdiB16</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x149</td>
							<td width="122" height="19"><a name="Ldb16_16">Ldb16_16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Ldb16_8">Ldb16_8</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x14a</td>
							<td width="122" height="19"><a name="Sta8_8">Sta8_8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x14b</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_A),L(R_MDR,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x14c</td>
							<td width="122" height="19"><a name="StaLo">StaLo</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">STLO,NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x14d</td>
							<td width="122" height="19"><a name="Sta8_16">Sta8_16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Sta8_8">Sta8_8</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x14e</td>
							<td width="122" height="19"><a name="Sta16_8">Sta16_8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x14f</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_A),L(R_MDR,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x150</td>
							<td width="122" height="19"><a name="Shi">Shi</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">STHI,NEXT(<a href="#StaLo">StaLo</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x151</td>
							<td width="122" height="19"><a name="Sta16_16">Sta16_16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Sta16_8">Sta16_8</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x152</td>
							<td width="122" height="19"><a name="Stb8_8">Stb8_8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x153</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#StaLo">StaLo</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x154</td>
							<td width="122" height="19"><a name="Stb8_16">Stb8_16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Stb8_8">Stb8_8</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x155</td>
							<td width="122" height="19"><a name="Stb16_8">Stb16_8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x156</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_B),L(R_MDR,LWORD),NEXT(<a href="#Shi">Shi</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x157</td>
							<td width="122" height="19"><a name="Stb16_16">Stb16_16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Stb16_8">Stb16_8</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x158</td>
							<td width="122" height="19"><a name="Sbc16">Sbc16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_SUB,WORD,CARRY_IN),L(R_A,LWORD),MISC(M_SET_FLAGS),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x159</td>
							<td width="122" height="19"><a name="Adc16">Adc16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_ADD,WORD,CARRY_IN),L(R_A,LWORD),MISC(M_SET_FLAGS),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x15a</td>
							<td width="122" height="19"><a name="LdaA_16">LdaA_16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#LdaA">LdaA</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x15b</td>
							<td width="122" height="19"><a name="LdaA">LdaA</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),L(R_A,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x15c</td>
							<td width="122" height="19"><a name="LdaB_16">LdaB_16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#LdaB">LdaB</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x15d</td>
							<td width="122" height="19"><a name="LdaB">LdaB</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_IR_BASE),L(R_B,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x15e</td>
							<td width="122" height="19"><a name="LdiA8">LdiA8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MDR),L(R_A,LBYTE),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x15f</td>
							<td width="122" height="19"><a name="LdiB8">LdiB8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MDR),L(R_B,LBYTE),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x160</td>
							<td width="122" height="19"><a name="LdiA16_lo">LdiA16_lo</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#LdiA16">LdiA16</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x161</td>
							<td width="122" height="19"><a name="LdiA16">LdiA16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MDR),L(R_A,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x162</td>
							<td width="122" height="19"><a name="LdiB16_lo">LdiB16_lo</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#LdiB16">LdiB16</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x163</td>
							<td width="122" height="19"><a name="LdiB16">LdiB16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MDR),L(R_B,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x164</td>
							<td width="122" height="19"><a name="LdiC16_lo">LdiC16_lo</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#LdiC16">LdiC16</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x165</td>
							<td width="122" height="19"><a name="LdiC16">LdiC16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MDR),L(R_C,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x166</td>
							<td width="122" height="19"><a name="RelBrLo">RelBrLo</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#RelBr">RelBr</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x167</td>
							<td width="122" height="19"><a name="RelBr">RelBr</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_PC),L(R_PC,LWORD),CODE,NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x168</td>
							<td width="122" height="19"><a name="CallImm">CallImm</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x169</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_PC),L(R_PC,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x16a</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_R(ER_MDR),E_L(R_PC),ALU(OP_SUB,WORD,NO_CARRY),L(R_MDR,LWORD),NEXT(<a href="#Push16">Push16</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x16b</td>
							<td width="122" height="19"><a name="CallA">CallA</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">DEC_TO_Z(R_SP),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x16c</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITELO,DEC_TO_Z(R_MAR),DATA,L(R_SP,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x16d</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITEHI,TO_Z(R_A),L(R_PC,LWORD),CODE,NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x16e</td>
							<td width="122" height="19"><a name="LdClr">LdClr</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READLO,NEXT(<a href="#FALLTHRU">FALLTHRU</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x16f</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MDR),L(R_A,LBYTE),NEXT(<a href="#Whi">Whi</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x170</td>
							<td width="122" height="19"><a name="Wcpte">Wcpte</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),MISC(M_LPTE),NEXT(<a href="#PCtoMAR">PCtoMAR</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x171</td>
							<td width="122" height="19"><a name="Enter">Enter</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x172</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_SP),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x173</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_SP),L(R_MDR,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x174</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">DEC_TO_Z(R_MAR),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x175</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITELO,DEC_TO_Z(R_MAR),DATA,L(R_SP,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x176</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITEHI,TO_Z(R_MAR),L(R_SP,LWORD),NEXT(<a href="#PCtoMAR">PCtoMAR</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x177</td>
							<td width="122" height="19"><a name="Bcopy">Bcopy</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">CBR(B_NEGATED,FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x178</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_B),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x179</td>
							<td width="122" height="19"></td>
							<td width="10" height="1">;</td>
							<td width="656" height="1">READLO,TO_Z(R_A),DATA,NEXT(<a href="#Bcopy0">Bcopy0</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x17a</td>
							<td width="122" height="19"><a name="ToSys">ToSys</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PRIV(1),CBR(B_NEGATED,FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x17b</td>
							<td width="122" height="19"></td>
							<td width="10" height="19"> ;</td>
							<td width="656" height="19">TO_Z(R_B),SET_ADR(DATA_SPACE,PTB_OVERRIDE),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x17c</td>
							<td width="122" height="19"></td>
							<td width="10" height="1">;</td>
							<td width="656" height="1">READLO,TO_Z(R_A),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x17d</td>
							<td width="122" height="19"><a name="Bcopy0">Bcopy0</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITELO,INC_TO_Z(R_MAR),L(R_A,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x17e</td>
							<td width="122" height="19"><a name="Bcopy1">Bcopy1</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">INC_TO_Z(R_B),L(R_B,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x17f</td>
							<td width="122" height="19"><a name="Bcopy2">Bcopy2</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">DEC_TO_Z(R_C),L(R_C,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x180</td>
							<td width="122" height="19"><a name="BackupPC">BackupPC</a></td>
							<td width="10" height="13">;</td>
							<td width="656" height="19">DEC_TO_Z(R_PC),L(R_PC,LWORD),CODE,NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x181</td>
							<td width="122" height="19"><a name="FromSys">FromSys</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PRIV(1),CBR(B_NEGATED,FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x182</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_B),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x183</td>
							<td width="122" height="19"></td>
							<td width="10" height="1">;</td>
							<td width="656" height="1">READLO,TO_Z(R_A),SET_ADR(DATA_SPACE,PTB_OVERRIDE),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x184</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITELO,INC_TO_Z(R_MAR),L(R_A,LWORD),NEXT(<a href="#Bcopy1">Bcopy1</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x185</td>
							<td width="122" height="19"><a name="Fault">Fault</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_MDR(R_MSW),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x186</td>
							<td width="122" height="19"></td>
							<td width="10" height="21">;</td>
							<td width="656" height="19">ZERO_TO_Z,MISC(M_LEI),LMODE(1),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x187</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">DEC_TO_Z(R_SSP),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x188</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x189</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x18a</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_MDR(R_SP),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x18b</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x18c</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x18d</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_MDR(R_TPC),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x18e</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x18f</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x190</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_MDR(R_A),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x191</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x192</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x193</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_MDR(R_B),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x194</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x195</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x196</td>
							<td width="122" height="19"></td>
							<td width="10" height="22">;</td>
							<td width="656" height="19">TO_MDR(R_C),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x197</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x198</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="21">0x199</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_MDR(R_DP),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x19a</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHLO,L(R_SP,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x19b</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">PUSHHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x19c</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_PC),L(R_A,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x19d</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_FCODE),DATA,L(R_C,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x19e</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x19f</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1a0</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">ZERO_TO_Z,L(R_DP,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1a1</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">FROM_MDR(R_PC),CODE,MISC(M_CLR_TRAP),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1a2</td>
							<td width="122" height="19"><a name="Reti">Reti</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_SP),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1a3</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1a4</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1a5</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">FROM_MDR(R_DP),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1a6</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1a7</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1a8</td>
							<td width="122" height="19"></td>
							<td width="10" height="23">;</td>
							<td width="656" height="19">FROM_MDR(R_C),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="22">0x1a9</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1aa</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1ab</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">FROM_MDR(R_B),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1ac</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1ad</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1ae</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">FROM_MDR(R_A),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1af</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1b0</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1b1</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">FROM_MDR(R_PC),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1b2</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1b3</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1b4</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MDR),MISC(M_COMMIT),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1b5</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">POPHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1b6</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READLO,INC_TO_Z(R_MAR),L(R_SP,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1b7</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MDR),L(R_MSW,LWORD),LMODE(1),LPAGING(1),MISC(M_LEI),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1b8</td>
							<td width="122" height="19"></td>
							<td width="10" height="17">;</td>
							<td width="656" height="19">TO_Z(R_TPC),L(R_SP,LWORD),NEXT(<a href="#PCtoMAR">PCtoMAR</a>)</td>

						</tr>

						<tr>

							<td width="41" height="23">0x1b9</td>
							<td width="122" height="19"><a name="Syscall">Syscall</a></td>
							<td width="10" height="17">;</td>
							<td width="656" height="19">TO_Z(R_MDR),L(R_A,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1ba</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">MISC(M_SYSCALL),NEXT(<a href="#Unreachable">Unreachable</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1bb</td>
							<td width="122" height="19"><a name="Ldcode8">Ldcode8</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDLO,NEXT(<a href="#LdiA8">LdiA8</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1bc</td>
							<td width="122" height="19"><a name="Wdpte">Wdpte</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),MISC(M_LPTE),NEXT(<a href="#PCtoMAR">PCtoMAR</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1bd</td>
							<td width="122" height="19"><a name="Shlb16">Shlb16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_B),E_R(ER_MDR),ALU(OP_ADD,WORD,NO_CARRY),L(R_B,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1be</td>
							<td width="122" height="19"><a name="Shla16">Shla16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_A),E_R(ER_MDR),ALU(OP_ADD,WORD,NO_CARRY),L(R_A,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1bf</td>
							<td width="122" height="19"><a name="Aluop16_16">Aluop16_16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Aluop16">Aluop16</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1c0</td>
							<td width="122" height="19"><a name="Cmpb16_16">Cmpb16_16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Cmpb16">Cmpb16</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1c1</td>
							<td width="122" height="19"><a name="Cmp16_16">Cmp16_16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">LDIMMLO,NEXT(<a href="#Cmp16">Cmp16</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1c2</td>
							<td width="122" height="19"><a name="PCtoMAR">PCtoMAR</a></td>
							<td width="8" height="19">;</td>
							<td width="656" height="19">TO_Z(R_PC),CODE,NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1c3</td>
							<td width="122" height="19"><a name="Vshl">Vshl</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">COMPARE_0(R_C),MISC(M_SET_FLAGS),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1c4</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">CBR(B_NEGATED,FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1c5</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">COMPARE_0(R_MDR),MISC(M_SET_FLAGS),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1c6</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">CBR(B_NEGATED,FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1c7</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_MDR),E_R(ER_MDR),ALU(OP_ADD,WORD,NO_CARRY),L(R_IR_REG,LWORD),NEXT(<a href="#Bcopy2">Bcopy2</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1c8</td>
							<td width="122" height="19"><a name="Vshr">Vshr</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">COMPARE_0(R_C),MISC(M_SET_FLAGS),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="1">0x1c9</td>
							<td width="122" height="19"></td>
							<td width="10" height="13">;</td>
							<td width="656" height="19">CBR(B_NEGATED,FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1ca</td>
							<td width="122" height="19"></td>
							<td width="8" height="19">;</td>
							<td width="656" height="19">COMPARE_0(R_MDR),MISC(M_SET_FLAGS),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1cb</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">CBR(B_NEGATED,FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1cc</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MDR),MISC(M_RSHIFT),L(R_IR_REG,LWORD),NEXT(<a href="#Bcopy2">Bcopy2</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1cd</td>
							<td width="122" height="19"><a name="LeaAAB2">LeaAAB2</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_R(ER_MDR),E_L(R_MDR),ALU(OP_ADD,WORD,NO_CARRY),L(R_MDR,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1ce</td>
							<td width="122" height="19"><a name="LeaA1">LeaA1</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_R(ER_MDR),E_L(R_A),ALU(OP_ADD,WORD,NO_CARRY),L(R_A,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1cf</td>
							<td width="122" height="19"><a name="LeaBBA2">LeaBBA2</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_R(ER_MDR),E_L(R_MDR),ALU(OP_ADD,WORD,NO_CARRY),L(R_MDR,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1d0</td>
							<td width="122" height="19"><a name="LeaB1">LeaB1</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_R(ER_MDR),E_L(R_B),ALU(OP_ADD,WORD,NO_CARRY),L(R_B,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1d1</td>
							<td width="122" height="19"><a name="LeaABA2">LeaABA2</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_R(ER_MDR),E_L(R_MDR),ALU(OP_ADD,WORD,NO_CARRY),L(R_MDR,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="23">0x1d2</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_R(ER_MDR),E_L(R_B),ALU(OP_ADD,WORD,NO_CARRY),L(R_A,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1d3</td>
							<td width="122" height="19"><a name="LeaBAB2">LeaBAB2</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_R(ER_MDR),E_L(R_MDR),ALU(OP_ADD,WORD,NO_CARRY),L(R_MDR,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1d4</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_R(ER_MDR),E_L(R_A),ALU(OP_ADD,WORD,NO_CARRY),L(R_B,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1d5</td>
							<td width="122" height="19"><a name="CopyMSWA">CopyMSWA</a></td>
							<td width="8" height="19">;</td>
							<td width="656" height="19">TO_Z(R_A),L(R_MSW,LWORD),LMODE(1),LPAGING(1),MISC(M_LEI),NEXT(<a href="#PCtoMAR">PCtoMAR</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1d6</td>
							<td width="122" height="19"><a name="Strcopy">Strcopy</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READLO,TO_Z(R_A),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1d7</td>
							<td width="122" height="19"></td>
							<td width="8" height="19">;</td>
							<td width="656" height="19">WRITELO,COMPARE8_0(R_MDR),MISC(M_SET_FLAGS),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1d8</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_PC),CODE,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1d9</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">INC_TO_Z(R_A),L(R_A,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1da</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">INC_TO_Z(R_B),L(R_B,LWORD),CBR(B_NEGATED,<a href="#BackupPC">BackupPC</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1db</td>
							<td width="122" height="19"><a name="LeaShort">LeaShort</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">GEN_ADDR(R_SP),L(R_IR_REG,LWORD),NEXT(<a href="#Fetch">Fetch</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1dc</td>
							<td width="122" height="19"><a name="Mcpy4">Mcpy4</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READHI,INC_TO_Z(R_MAR),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1dd</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READLO,TO_Z(R_B),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1de</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_MDR),L(R_C,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1df</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READHI,INC_TO_Z(R_MAR),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1e0</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READLO,TO_Z(R_A),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1e1</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITEHI,INC_TO_Z(R_MAR),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1e2</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITELO,INC_TO_Z(R_MAR),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1e3</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">TO_Z(R_C),L(R_MDR,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1e4</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITEHI,INC_TO_Z(R_MAR),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1e5</td>
							<td width="122" height="19"></td>
							<td width="8" height="19">;</td>
							<td width="656" height="19">WRITELO,INC_TO_Z(R_MAR),L(R_A,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="13">0x1e6</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">INC2_TO_Z(R_B),L(R_B,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1e7</td>
							<td width="122" height="19"></td>
							<td width="8" height="19">;</td>
							<td width="656" height="19">INC2_TO_Z(R_B),L(R_B,LWORD),NEXT(<a href="#PCtoMAR">PCtoMAR</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1e8</td>
							<td width="122" height="19"><a name="Mop16">Mop16</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1e9</td>
							<td width="122" height="19"></td>
							<td width="8" height="19">;</td>
							<td width="656" height="19">WRITELO,DEC_TO_Z(R_MAR),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1ea</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1eb</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITEHI,TO_Z(R_MDR),L(R_C,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1ec</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">DEC_TO_Z(R_B),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1ed</td>
							<td width="122" height="19"></td>
							<td width="8" height="19">;</td>
							<td width="656" height="19">READLO,DEC_TO_Z(R_MAR),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1ee</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READHI,TO_Z(R_MAR),L(R_B,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1ef</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_C),E_R(ER_MDR),ALU(OP_IR13,WORD,NO_CARRY),L(R_MDR,LWORD),MISC(M_SET_FLAGS),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1f0</td>
							<td width="122" height="19"><a name="Mop16a">Mop16a</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">DEC_TO_Z(R_A),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1f1</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITELO,DEC_TO_Z(R_MAR),DATA,L(R_A,LWORD),NEXT(<a href="#Whi">Whi</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1f2</td>
							<td width="122" height="19"><a name="Mop16Carry">Mop16Carry</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READLO,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1f3</td>
							<td width="122" height="19"></td>
							<td width="8" height="19">;</td>
							<td width="656" height="19">WRITELO,DEC_TO_Z(R_MAR),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1f4</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1f5</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">WRITEHI,TO_Z(R_MDR),L(R_C,LWORD),READHI,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1f6</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">DEC_TO_Z(R_B),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1f7</td>
							<td width="122" height="19"></td>
							<td width="8" height="19">;</td>
							<td width="656" height="19">READLO,DEC_TO_Z(R_MAR),DATA,NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1f8</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">READHI,TO_Z(R_MAR),L(R_B,LWORD),NEXT(FALLTHRU)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1f9</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">E_L(R_C),E_R(ER_MDR),ALU(OP_IR13,WORD,CARRY_IN),L(R_MDR,LWORD),MISC(M_SET_FLAGS),NEXT(<a href="#Mop16a">Mop16a</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1fa</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19"></td>

						</tr>

						<tr>

							<td width="41" height="19">0x1fb</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19"></td>

						</tr>

						<tr>

							<td width="41" height="19">0x1fc</td>
							<td width="235" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19"></td>

						</tr>

						<tr>

							<td width="41" height="19">0x1fd</td>
							<td width="122" height="19"></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19"></td>

						</tr>

						<tr>

							<td width="41" height="19">0x1fe</td>
							<td width="122" height="19"><a name="Unreachable">Unreachable</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19">NEXT(<a href="#Unreachable">Unreachable</a>)</td>

						</tr>

						<tr>

							<td width="41" height="19">0x1ff</td>
							<td width="122" height="19"><a name="UNUSABLE">UNUSABLE</a></td>
							<td width="10" height="19">;</td>
							<td width="656" height="19"></td>

						</tr>

</table>
