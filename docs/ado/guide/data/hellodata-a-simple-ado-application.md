---
title: "HelloData:는 간단한 ADO 응용 프로그램 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a1c7d61c6349945274febc92e4e6b5acfcc379b9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="hellodata-a-simple-ado-application"></a>HelloData:는 간단한 ADO 응용 프로그램
이 간단한 응용 프로그램을 4 개의 주요 ADO 작업의 각 단계별로: 가져오기, 검사, 편집 및 데이터를 업데이트 합니다. 이러한 작업은 Microsoft® SQL Server에 포함 된 Northwind 샘플 데이터베이스에 대해 수행 됩니다. ADO의 기본 사항에 집중 하 고 코드 혼란을 방지 하기 위해이 예제에서 오류 처리는 최소화 됩니다.  
  
### <a name="to-run-hellodata"></a>HelloData를 실행 하려면  
  
1.  ADO 라이브러리 참조 하는 새 표준 EXE Visual Basic 프로젝트를 만듭니다. 자세한 내용은 참조 [ADO 라이브러리 참조](../../../ado/guide/referencing-the-ado-libraries.md)합니다.  
  
2.  폼의 위쪽에 명령 단추 4 개를 만들기는 **이름** 및 **캡션** 속성을이 항목의 끝에 있는 테이블에 표시 된 값입니다.  
  
3.  아래 단추를 추가 **Microsoft DataGrid 컨트롤** (Msdatgrd.ocx). Msdatgrd.ocx 파일 Visual Basic을 사용한에 포함 되며 \windows\system32 또는 \winnt\system32 디렉터리에 위치 합니다. Visual Basic 도구 상자 창에 DataGrid 컨트롤을 추가 하려면 선택 **구성 요소 중... ** 에서 **프로젝트** 메뉴. 다음의 확인란 옆에 "합니다 (SP3) (OLEDB)"을 클릭 한 다음 **확인**합니다. 컨트롤 프로젝트를 추가 하려면 도구 상자에서 DataGrid 컨트롤을 Visual Basic 폼으로 끕니다.  
  
4.  만들기는 **TextBox** 표 아래의 폼에 테이블에 표시 된 대로 속성을 설정 합니다. 양식을 완료 했으면 다음 그림을 비슷해야 합니다.  
  
5.  마지막으로에 나열 된 코드를 복사 [HelloData 코드](../../../ado/guide/data/hellodata-code.md), 폼의 코드 편집기 창에 붙여 넣습니다. 키를 눌러 **F5** 코드를 실행 합니다.  
  
> [!NOTE]
>  다음 예제에서는 및의 가이드는 서버 인증에 사용자 id "MyId" 암호로 "123aBc"를 사용 하 게 됩니다. 서버에 대 한 유효한 로그온 자격 증명을 사용 하 여 이러한 값으로 바꿔야 합니다. 또한 서버 이름 사용 하 여 "MySQLServer" 값을 대체 합니다.  
  
 에 대 한 자세한 설명은 코드를 참조 하세요. [HelloData에 대 한 의견](../../../ado/guide/data/comments-on-hellodata.md)합니다.  
  
 ![Form1 HelloData VB 응용 프로그램에 대 한 표시](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|컨트롤 형식|속성|값|  
|------------------|--------------|-----------|  
|Form|이름|Form1|  
||높이|6500|  
||너비|6500|  
|MS DataGrid|이름|grdDisplay1|  
|TextBox|이름|txtDisplay1|  
||여러 줄|true|  
|명령 단추|이름|cmdGetData|  
||캡션|Get Data|  
|명령 단추|이름|cmdExamineData|  
||캡션|데이터를 검사 합니다.|  
|명령 단추|이름|cmdEditData|  
||캡션|데이터 편집|  
|명령 단추|이름|cmdUpdateData|  
||캡션|업데이트 데이터|
