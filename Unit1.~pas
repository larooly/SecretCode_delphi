unit Unit1;

interface

uses
  Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
  Dialogs, StdCtrls;

type
  TForm1 = class(TForm)
    Label1: TLabel;
    Label3: TLabel;
    Edit1: TEdit;
    Edit3: TEdit;
    Memo1: TMemo;
    Memo3: TMemo;
    Button1: TButton;
    Button3: TButton;
    Label4: TLabel;
    Label5: TLabel;
    Label6: TLabel;
    Label7: TLabel;
    Label8: TLabel;
    Label9: TLabel;
    Label10: TLabel;
    Label11: TLabel;
    Button2: TButton;
    procedure Button1Click(Sender: TObject);
    procedure Button3Click(Sender: TObject);
    procedure Button2Click(Sender: TObject);
  private
    { Private declarations }
  public
    { Public declarations }
  end;

var
  Form1: TForm1;

implementation

{$R *.dfm}
function dodo(a,b : integer): integer;
var
  i : Integer;
  c: Integer;
begin
  C:=1;
  for i:=0 to b-1 do
  begin
    c:=c*a;
  end;
  Result:= C;
end;  //너무작다

function dodo2(a,b : Int64): Uint64;
var
  i : Integer;
  c: UInt64;
begin
  C:=1;
  for i:=0 to b-1 do
  begin
    c:=c*a;
  end;
  Result:= C;
end;

//10,String->number
function ChanStringto10num(a : String):integer;   //A->65(10진수숫자)
var
  aki : String;
  num : integer;
begin
  aki :=' !"#$%&''()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}';
  num := Pos(a,aki)+31;
  result:= num;//여기는 정직하게1부터시작이다    Copy(aki,a+1,1);
end;
//65->A
function Chan10toStringnum(a : integer):String;   //65->A(10진수숫자->Dec)
var
  aki : String;
  num : String;
begin
  aki :=' !"#$%&''()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}';
  num := Copy(aki,a-31,1);
  result:= num;//여기는 정직하게1부터시작이다    Copy(aki,a+1,1);
end;
//이걸쓰면 되겠다.



//16->10short
function ShortChan16to10(num : String):integer;
var
  st16 : string;
begin
  st16 := '0123456789ABCDEF';
  Result := Pos(num,st16)-1;
end;
//10->16short
function ShortChan10to16(num : integer):string;
var
  st16 : string;
begin
  st16 := '0123456789ABCDEF';
  Result := Copy(st16,num+1,1);
end;
//10->16Long 한글자만
function LongChan10to16(num : Uint64):string;
var
  i : integer;
  mok , namugi : Uint64;
  mem : TMemo;
  s : String;
begin
  mem := Form1.Memo3;
  mem.Clear;
  while true do
  begin
    mok := num div 16;
    namugi := num mod 16;
    s:= '';
    mem.Lines.Add(ShortChan10to16(namugi));
    num:= mok;
    if mok =0 then
    begin
      for i :=0 to mem.Lines.Count-1 do
      begin
        s:= mem.Lines[i]+s;
      end;
      Result := S;
      break;
    end;
  end;
end;
//여러글자가 들어갔을때
function LongLongChan10to16(word : string):string;
var
  num : Uint64;
  ss : String;
  i : integer;
begin
  ss:= '';
  num := length(word);
  for i:= 1 to num do
  begin
    ss:= ss+LongChan10to16(ChanStringto10num(Copy(word,i,1)));
  end;
  Result := ss;
end;
/////////16->10으로바꾸는법(62체인지용)
function Kill16to10for62(qu : string):Uint64;
var
  i  : integer;
  sum : Uint64;
begin
  sum := 0;
  for i :=1 to length(qu) do
  begin
    //생각잘해라 앞에서부터 역산하면 어떻게되는지
    sum:= sum+(ShortChan16to10(qu[i]))*dodo2(16,length(qu)-i);
  end;
  Result := sum;
end;//이제이걸 62로 바꾸면 된다.
//=============저번거 ======================

///////간단하게//////////////////////
function SimChange(a : string):integer; overload;//62->10
var
  aki : String;
begin
  aki :='0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
  result:= Pos(a,aki)-1;//여기는 정직하게1부터시작이다
end;
function SimChange(a : integer):string; overload;//10->62
var
  aki : String;
begin
  aki :='0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
  result:= Copy(aki,a+1,1);//여기는 정직하게1부터시작이다
end;
///////바꿔보자//////////////////////
function Div10to62(a : UInt64): String; //10->62로바꾸기
var
  mem : TMemo;
  i: Integer;//몫 나머지 루 프
  mok , na : Uint64;
  s : String;
begin
  mem := Form1.Memo1;
  mem.Clear;
  while true do
  begin
    mok := a div 62;
    na := a mod 62;

    mem.Lines.Add(inttostr(na));//나머지를 저장
    a:= mok;
    if mok= 0 then
    begin
      s:='';
      for i := 0 to mem.Lines.Count-1 do
      begin
        s:= SimChange(strtoint(mem.lines[i]))+s;   //s:= changeItoS(mem.lines[i])+s;
      end;
      Result := s;
      break;
    end;
  end
end;


function Div62to10(a : String): UInt64;
var
  i : integer;
  mem : TMemo;
  sum : Uint64;
begin
  mem := Form1.Memo3;
  mem.Clear;
  for i := 1 to length(a) do
  begin
    Mem.Lines.Add(Copy(a ,i,1));
  end;
  sum :=0;
  for i := 0 to Mem.Lines.Count-1 do
  begin
    sum:= sum+SimChange(mem.Lines[i])*(dodo2(62,Mem.Lines.Count-1-i));//sum+changeStoI(mem.Lines[i])*(dodo(62,Mem.Lines.Count-1-i))
  end;
  Result:= sum;
end;
//=============여기까지가 저번거======================

//천천히 조심히 바꿔
//나누자 두개로 하나는 두글자용 하나느 통짜용
function two16to10(a : string):String;  //절대 두자리만 넣어라
var
  sum : Integer;
begin
  sum :=0;
  sum:= ShortChan16to10(a[1])*16+ShortChan16to10(a[2]);
  //41->65->A
  Result:= Chan10toStringnum(sum);
   //리얼16->10으로바꾸기
end;


/////////16 to 문자열로 바꾸기
function Chan16to10(word16 : String): String;   //2개짜리랑 통짜랑 나눠야할듯
var
  wf16 : String;      //16진수 값이 들어감
  i : integer;
begin
//두자리씩 잘라서 바꿔야함
  wf16 := '';
  for i := 1 to (length(word16) div 2) do   //천천히 생각해라
  begin
    wf16 := wf16+ two16to10(copy(word16,i*2-1,2));
  end;
  Result := wf16;
end;

////////////////16진법말고 찐문자열

procedure TForm1.Button1Click(Sender: TObject);
begin
  Label5.Caption := LongLongChan10to16(edit1.Text);
  Label7.Caption := Div10to62(Kill16to10for62(LongLongChan10to16(edit1.Text)));//inttostr(ShortChan16to10('A') )
end;

procedure TForm1.Button3Click(Sender: TObject);
begin
  Label9.Caption := LongChan10to16(Div62to10(Edit3.Text));//16진수가 나옴 이걸10으로 바꾸면 됨
  Label11.Caption := Chan16to10(LongChan10to16(Div62to10(Edit3.Text)));
end;

procedure TForm1.Button2Click(Sender: TObject);
begin
  Edit3.Text := Label7.Caption;
  Label9.Caption := LongChan10to16(Div62to10(Edit3.Text));//16진수가 나옴 이걸10으로 바꾸면 됨
  Label11.Caption := Chan16to10(LongChan10to16(Div62to10(Edit3.Text)));
end;

end.
   //Label2.Caption :=inttostr(Div62to10(Edit3.Text));//여긴 맞음
   //label9.Caption:= inttostr(Div62to10(Edit3.Text));//이걸쓰면 간단히 가능할듯?
  //label9.Caption:= inttostr(Div62to10(Edit3.Text));//이걸쓰면 간단히 가능할듯?
  //Label2.Caption :=inttostr(Div62to10(Edit3.Text));//여긴 맞음
  //Label12.Caption := inttostr(Kill16to10for62('31202B'));
  //Label12.Caption := inttostr(Kill16to10for62(LongLongChan10to16(edit1.Text)));