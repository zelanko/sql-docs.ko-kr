---
title: 지원 되는 Access 보고서 기능 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], Access reports
- functions [Reporting Services]
- controls [Reporting Services]
- Access reports [Reporting Services]
- properties [Reporting Services], Access reports
- importing reports
- modules [Reporting Services]
ms.assetid: 7ffec331-6365-4c13-8e58-b77a48cffb44
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ae982257f0be29103803a7d036142f58a50f1a04
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59933105"
---
# <a name="supported-access-report-features-ssrs"></a>지원되는 Access 보고서 기능(SSRS)
  보고서 디자이너로 보고서를 가져오는 과정에서 [!INCLUDE[msCoName](../includes/msconame-md.md)] Access 보고서가 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] RDL(Report Definition Language) 파일로 변환됩니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 Access의 여러 기능을 지원하지만 Access와 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 차이로 인해 일부 항목이 약간 수정되거나 지원되지 않을 수 있습니다. 이 항목에서는 Access 보고서 기능이 RDL로 변환되는 방법에 대해 설명합니다.  
  
## <a name="importing-access-reports"></a>Access 보고서 가져오기  
 일부 쿼리에는 Access 고유의 코드가 포함됩니다. Access 코드는 보고서와 함께 가져올 수 없습니다. 또한 쿼리에 포함된 문자열이 있으면 보고서를 제대로 가져오지 못할 수 있습니다. 이 문제를 해결하려면 문자열을 문자 코드로 바꿉니다. 예를 들어 쉼표(,)를 CHAR(34)로 바꿉니다.  
  
 가져오기 프로세스에서 세미콜론 (;)를 제대로 전달 하지 않습니다 또는 XML 태그 문자 (\<, > 등)에서 연결 문자열 정보. 연결 문자열에 세미콜론이나 XML 태그 문자가 있으면 보고서를 가져온 후 새 보고서에서 암호를 수동으로 설정해야 합니다.  
  
 가져오기 과정에서는 연결 문자열의 연결 설정이나 일반 시간 제한 설정을 가져올 수 없습니다. 보고서를 가져온 후 이러한 설정을 조정해야 합니다.  
  
 쿼리에 매개 변수가 포함된 보고서를 가져오는 경우에는 보고서를 가져올 때 쿼리가 변환되지 않습니다. 보고서와 함께 쿼리를 가져오려면 임시로 Access 보고서의 쿼리 매개 변수를 하드 코드 값으로 바꾸고 보고서를 가져온 후 쿼리 매개 변수로 다시 바꿉니다.  
  
## <a name="page-layout"></a>페이지 레이아웃  
 Page layout in Access의 페이지 레이아웃은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]와 다릅니다. Access에서는 "밴드"를 사용하여 페이지의 항목이 정렬되므로 페이지 구역이 세로로 배열됩니다. 이러한 구역에는 보고서 머리글, 보고서 바닥글, 페이지 머리글, 페이지 바닥글, 그룹 및 자세한 정보가 포함될 수 있습니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 레이아웃을 좀 더 유연하게 조정할 수 있습니다. 데이터 영역은 그룹화 및 자세한 정보를 제공하므로 보고서 본문의 어느 부분에나 여러 데이터 영역을 놓고 나란히 배열할 수도 있습니다. 또한 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에는 Access의 페이지 머리글 및 바닥글과 유사한 "밴드" 페이지 머리글 및 바닥글이 포함됩니다.  
  
 Access의 보고서를 보고서 디자이너로 가져오면 Access 보고서의 페이지 머리글과 바닥글이 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서의 페이지 머리글과 바닥글로 변환됩니다. 그룹과 자세한 정보는 목록 데이터 영역으로 변환됩니다. 보고서 머리글과 바닥글은 개별 밴드가 아닌 보고서 본문에 위치합니다. 따라서 항목 위치가 Access 보고서에서의 위치와 약간 다를 수 있습니다.  
  
> [!NOTE]  
>  일부 Access 보고서에서 서로 인접한 보고서 항목이 실제로 겹칠 수 있습니다. 보고서 디자이너를 사용하여 보고서를 가져오는 경우 겹치는 부분이 수정되지 않아 보고서를 실행할 때 예기치 않은 결과가 나타날 수 있습니다.  
  
## <a name="data-sources"></a>솔루션 탐색기  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]와 같은 OLE DB 데이터 원본을 지원합니다. Access 프로젝트 파일(.adp)에서 보고서를 가져오는 경우에는 데이터 원본에 대한 연결 문자열을 .adp 파일의 연결 문자열에서 가져옵니다. Access 데이터베이스 파일(.mdb 또는 .accdb)에서 보고서를 가져오는 경우에는 연결 문자열이 Access 데이터베이스를 가리키므로 보고서를 가져온 후 연결 문자열을 수정해야 합니다. Access 보고서에 대한 데이터 원본이 쿼리이면 쿼리 정보가 수정되지 않고 RDL에 저장됩니다. Access 보고서에 대한 데이터 원본이 테이블이면 변환 과정에서 테이블 이름과 테이블의 필드를 기반으로 쿼리가 생성됩니다.  
  
## <a name="reports-with-custom-modules"></a>사용자 지정 모듈이 있는 보고서  
 있으면 사용자 지정 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 모듈 내에 포함 된 코드 변환 되지 않습니다. 경고가 생성 되 고 표시 코드 가져오기 프로세스 중 발생 하는 보고서 디자이너에는 **작업 목록** 창입니다.  
  
## <a name="report-controls"></a>보고서 컨트롤  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 다음 Access 컨트롤을 지원하고 변환된 보고서 정의에 포함합니다.  
  
|||||  
|-|-|-|-|  
|image|레이블|선|직사각형|  
|SubForm|SubReport<br /><br /> **참고** SubReport 컨트롤은 주 보고서 내에서 변환, 하위 보고서 자체는 별도로 변환 됩니다.|TextBox||  
  
 다음 컨트롤은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 지원되지 않습니다.  
  
|||||  
|-|-|-|-|  
|BoundObjectFrame|CheckBox|ComboBox|CommandButton|  
|CustomControl|ListBox|ObjectFrame|OptionButton|  
|TabControl|ToggleButton|||  
  
 경고가 생성 되 고 표시 발견 되 면 이러한 컨트롤이 가져오기 프로세스 중에 **작업 목록** 창입니다.  
  
 ActiveX, Office Web Components 등의 다른 컨트롤은 가져올 수 없습니다. 예를 들어 Access 보고서에 OWC 차트 컨트롤이 있는 경우 보고서를 가져올 때 이 컨트롤은 변환되지 않습니다.  
  
## <a name="report-properties"></a>보고서 속성  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 Access 사용자 인터페이스를 통해 사용할 수 있는 다음 속성을 지원합니다. 코드에서만 사용할 수 있는 속성은 지원되지 않으므로 다음 목록에서 제외되었습니다.  
  
|||||  
|-|-|-|-|  
|BackColor|BackStyle|BorderColor|BorderStyle|  
|BorderWidth|BottomMargin|CanGrow(입력란)|CanShrink(입력란)|  
|캡션|FontBold|FontItalic|FontName|  
|FontSize|FontUnderline|FontWeight|ForceNewPage|  
|ForeColor|높이|HideDuplicates|Hyperlink|  
|IsHyperlink|IsVisible|KeepTogether(그룹)|왼쪽|  
|LeftMargin|LineSlant|LineSpacing|LinkChildFields|  
|LinkMasterFields|NewRowOrCol|PageFooter|PageHeader|  
|인쇄할 페이지|Picture|PictureTiling(보고서)|ReadingOrder|  
|RepeatSection|RightMargin|RunningSum|SizeMode|  
|TextAlign|TOP|TopMargin|너비|  
  
 Access 사용자 인터페이스를 통해 사용할 수 있는 다음 속성은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 지원되지 않습니다.  
  
|||||  
|-|-|-|-|  
|CanGrow(구역)|CanShrink(구역)|DecimalPlaces|FastLaserPrinting|  
|Assert|FilterOn|형식|FormatConditions|  
|GrpKeepTogether|KeepTogether(구역)|NumeralShapes|방향|  
|PaintPalette|PaletteSource|PictureAlignment|PicturePages|  
|PictureSizeMode|PictureTiling(이미지)|ScrollBars|SpecialEffect|  
|세로||||  
  
## <a name="grouping"></a>그룹화  
 Access에서는 그룹 식, `GroupOn` 속성 및 `GroupInterval` 속성의 세 가지 속성을 조합하여 그룹 수준을 정의합니다. 그룹 머리글이나 바닥글이 없는 그룹은 해당 그룹에 포함된 그룹과 병합됩니다. 그룹에 다른 그룹이 포함되어 있지 않으면 세부 구역에 정렬이 적용되고 그룹이 삭제됩니다.  
  
## <a name="expressions"></a>식  
 Access에서는 식을 사용하여 입력란에 나타나는 값을 지정합니다. 또한 일부 집계 함수뿐만 아니라 식 언어로 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]을 사용합니다. 보고서 디자이너에서는 이러한 Access 식을 보고서 식으로 변환합니다.  
  
### <a name="functions"></a>함수  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 정의는 기본 식 언어로 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET을 사용하지만 Access 2002에서는 Visual Basic을 사용합니다. 다음 목록에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 지원되는 함수를 설명합니다.  
  
#### <a name="array-functions"></a>배열 함수  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 다음 배열 함수를 지원합니다.  
  
-   LBound  
  
-   UBound  
  
#### <a name="conversion-functions"></a>변환 함수  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 다음 변환 함수를 지원합니다.  
  
|||||  
|-|-|-|-|  
|Asc|CBool|CByte|CCur|  
|CDate|CDbl|CDec|Chr|  
|Chr$|CInt|CLng|CSng|  
|CStr|CVar|CVDate|형식|  
|FormatCurrency|FormatDateTime|FormatNumber|FormatPercent|  
|Hex|Hex$|Nz|Oct|  
|Oct$|Str|Str$|StrConv|  
|Val||||  
  
 다음 변환 함수는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 지원되지 않습니다.  
  
-   GUIDFromString  
  
-   StringFromGUID  
  
#### <a name="database-functions"></a>데이터베이스 함수  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 다음 데이터베이스 함수를 지원합니다.  
  
|||||  
|-|-|-|-|  
|CreateReport|GetObject|HyperlinkPart|Partition|  
  
 다음 데이터베이스 함수는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 지원되지 않습니다.  
  
|||||  
|-|-|-|-|  
|CodeDb|CreateControl|CreateForm|CreateGroupLevel|  
|CreateObject 메서드|CreateReportControl|CurrentDb|CurrentUser|  
|DeleteControl|DeleteReportControl|Eval|IMEStatus|  
|SysCmd||||  
  
#### <a name="datetime-functions"></a>날짜/시간 함수  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 다음 날짜/시간 함수를 지원합니다.  
  
|||||  
|-|-|-|-|  
|Date|Date$|DateAdd|DateDiff|  
|DatePart|DateSerial|DateValue|Day|  
|Hour|Minute|Month|MonthName|  
|지금|Second|Time|Time$|  
|Timer|TimeSerial|TimeValue|Weekday|  
|WeekdayName|Year|||  
  
#### <a name="ddeole-functions"></a>DDE/OLE 함수  
 다음 DDE/OLE 함수는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 지원되지 않습니다.  
  
|||||  
|-|-|-|-|  
|DDE|DDEIntitate|DDERequest|DDESend|  
|LoadPicture||||  
  
#### <a name="domain-aggregate-functions"></a>도메인 집계 함수  
 다음 도메인 집계 함수는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 지원되지 않습니다.  
  
|||||  
|-|-|-|-|  
|DAvg|DCount|DFirst|DLast|  
|DLookup|DMax|DMin|DStDev|  
|DStDevP|DSum|DVar|DVarP|  
  
#### <a name="error-handling-functions"></a>오류 처리 함수  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 다음 오류 처리 함수를 지원합니다.  
  
|||||  
|-|-|-|-|  
|Err|Error|Error$|IsError|  
  
 다음 오류 처리 함수는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 지원되지 않습니다.  
  
-   CVErr  
  
#### <a name="financial-functions"></a>재무 함수  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 다음 재무 함수를 지원합니다.  
  
|||||  
|-|-|-|-|  
|DDB|FV|IPmt|IRR|  
|MIRR|NPer|NPV|Pmt|  
|PPmt|PV|Rate|SLN|  
|SYD||||  
  
#### <a name="interaction-functions"></a>상호 작용 함수  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 다음 상호 작용 함수를 지원합니다.  
  
|||||  
|-|-|-|-|  
|Command|Command$|CurDir|CurDir$|  
|DeleteSetting|Dir|Dir$|Environ|  
|Environ$|EOF|FileAttr|FileDateTime|  
|FileLen|FreeFile|GetAllSettings|GetAttr|  
|GetSetting|Loc|LOF|QBColor|  
|RGB|SaveSetting|검색|SetAttr|  
|Shell|Spc|탭||  
  
 다음 상호 작용 함수는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 지원되지 않습니다.  
  
|||||  
|-|-|-|-|  
|DoEvents|입력|입력|Input$|  
  
#### <a name="inspection-functions"></a>검사 함수  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 다음 검사 함수를 지원합니다.  
  
|||||  
|-|-|-|-|  
|IsArray|IsDate|IsEmpty|IsError|  
|IsNull|IsNumeric|IsObject|TypeName|  
|VarType||||  
  
 다음 검사 함수는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 지원되지 않습니다.  
  
-   IsMissing  
  
#### <a name="math-functions"></a>수치 연산 함수  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 다음 수치 연산 함수를 지원합니다.  
  
|||||  
|-|-|-|-|  
|Abs|Atn|Cos|Exp|  
|Fix|Int|Log|Rnd|  
|반올림|Sgn|Sin|Sqr|  
|Tan||||  
  
#### <a name="message-functions"></a>메시지 함수  
 다음 메시지 함수는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 지원되지 않습니다.  
  
|||||  
|-|-|-|-|  
|InputBox|InputBox$|MsgBox||  
  
#### <a name="program-flow-functions"></a>프로그램 흐름 함수  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 다음 프로그램 흐름 함수를 지원합니다.  
  
|||||  
|-|-|-|-|  
|Choose|IIf|스위치||  
  
#### <a name="sql-aggregate-functions"></a>SQL 집계 함수  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 다음 SQL 집계 함수를 지원합니다.  
  
|||||  
|-|-|-|-|  
|Avg|개수|최대값|최소값|  
|StDev|StDevP|합계|Var|  
|VarP||||  
  
#### <a name="text-functions"></a>텍스트 함수  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 다음 텍스트 함수를 지원합니다.  
  
|||||  
|-|-|-|-|  
|형식|Format$|InStr|InStrRev|  
|LCase|LCase$|왼쪽|Left$|  
|Len|LTrim|LTrim$|Mid|  
|Mid$|바꾸기|오른쪽|Right$|  
|RTrim|공백|Space$|StrComp|  
|StrConv|문자열|String$|StrReverse|  
|Trim|Trim$|UCase|UCase$|  
  
### <a name="constants"></a>상수  
 Access에서는 `vbTrue` 등의 특수한 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 상수를 지원하지 않으므로 변환이 필요하지 않습니다. 그러나 예외 사항이 하나 있습니다. 키워드 `Null`은 `System.DbNull.Value`로 변환됩니다.  
  
### <a name="parameters"></a>매개 변수  
 보고서 디자이너는 가져오기 과정에서 보고서의 모든 식을 검색하여 필드 이름이나 컨트롤에 해당하지 않는 변수가 있는지 확인합니다. 이러한 변수는 보고서 매개 변수에 추가됩니다.  
  
 저장 프로시저 매개 변수의 데이터 형식은 항상 문자열로 가져옵니다. 보고서를 가져온 후 올바른 데이터 형식을 사용하려면 수동으로 매개 변수를 변경해야 합니다.  
  
### <a name="object-names"></a>개체 이름  
 Access에서는 필드 이름이 컨트롤 이름과 동일할 수 있지만 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 그렇지 않습니다. 또한 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 6.0에서는 변수 이름에 공백을 사용할 수 있지만 Visual Basic .NET에서는 그렇지 않습니다. 가져오기 과정에서 이러한 개체의 이름은 모두 유효한 이름으로 바뀌며 여러 개체의 이름이 같은 경우 고유한 이름이 할당됩니다. 각 식이 검색되어 이름이 바뀐 개체에 해당하는 변수의 이름이 새 이름으로 바뀝니다.  
  
## <a name="rectangles-and-containment"></a>사각형 및 포함  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 정의에서는 사각형에 다른 보고서 항목이 포함될 수 있습니다. 보고서 항목보다 크고 해당 영역의 90% 이상과 겹치는 사각형은 모두 보고서 항목의 컨테이너가 됩니다.  
  
## <a name="bitmaps"></a>비트맵  
 보고서에 포함된 비트맵은 초기 형식에 관계없이 보고서를 가져올 때 모두 .bmp 형식으로 변환됩니다. 예를 들어 보고서에 .jpg 및 .gif 파일이 있는 경우 보고서와 함께 가져오는 리소스는 .bmp 파일이 됩니다. 비트맵은 포함 이미지로 보고서에 저장됩니다. 포함 이미지에 대 한 정보를 참조 하세요 [이미지 &#40;보고서 작성기 및 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)합니다.  
  
## <a name="other-considerations"></a>기타 고려 사항  
 Access에서 보고서를 가져올 때는 위의 항목뿐만 아니라 다음 사항도 적용됩니다.  
  
-   조건부 서식은 변환되지 않습니다.  
  
-   Access의 보고서 속성에 있는 설명 필드는 변환되지 않습니다.  
  
  
