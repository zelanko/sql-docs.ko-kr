---
title: 'HelloData: 간단한 ADO 응용 프로그램을 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed92b3f83e865d2b8d4f3e3a3a3cb95e291d771e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63162103"
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData: 간단한 ADO 애플리케이션
각각 4 개의 주요 ADO 작업을 통해이 간단한 응용 프로그램 단계: 가져오기, 검사, 편집 및 데이터를 업데이트 합니다. 이러한 작업은 Microsoft® SQL Server에 포함 된 Northwind 샘플 데이터베이스에 대해 수행 됩니다. ADO의 기본 사항에 집중 하 고 코드 혼란을 방지 하기 위해이 예제에서 오류 처리는 최소화 됩니다.  
  
### <a name="to-run-hellodata"></a>HelloData를 실행 하려면  
  
1.  ADO 라이브러리 참조 하는 새 표준 EXE Visual Basic 프로젝트를 만듭니다. 자세한 내용은 [ADO 라이브러리 참조](../../../ado/guide/referencing-the-ado-libraries.md)합니다.  
  
2.  폼의 맨 위에 있는 명령 단추 4 개를 만듭니다는 **이름** 하 고 **캡션** 속성을이 항목의 끝에 있는 표에 표시 된 값.  
  
3.  단추 아래에서 추가 된 **Microsoft DataGrid 컨트롤** (Msdatgrd.ocx). Msdatgrd.ocx 파일을 Visual Basic을 사용한 포함 되어 있으며 \windows\system32 또는 \winnt\system32 디렉터리에. Visual Basic 도구 상자 창에 DataGrid 컨트롤을 추가 하려면 **구성 하는 중...**  에서 합니다 **프로젝트** 메뉴. 확인란 옆에 "Microsoft DataGrid 컨트롤 (SP3) 6.0 (OLEDB)"을 클릭 한 다음 **확인**합니다. 컨트롤 프로젝트에 추가할 DataGrid 컨트롤을 도구 상자에서 Visual Basic 폼으로 끕니다.  
  
4.  만들기는 **텍스트 상자** 표 아래의 양식의 표에 나와 있는 것 처럼 해당 속성을 설정 합니다. 폼을 완료 했으면 다음 그림을 비슷해야 합니다.  
  
5.  마지막으로,에 나열 된 코드를 복사 [HelloData 코드](../../../ado/guide/data/hellodata-code.md), 폼의 코드 편집기 창에 붙여 넣습니다. 키를 눌러 **F5** 코드를 실행 합니다.  
  
> [!NOTE]
>  다음 예제에서는 및 가이드 전체에서 사용자 id "MyId" 암호를 사용 하 여 "123aBc"는 서버 인증에 사용 됩니다. 서버에 대해 유효한 로그온 자격 증명을 사용 하 여 이러한 값으로 바꿔야 합니다. 또한 대체 서버의 이름 사용 하 여 "MySQLServer" 값입니다.  
  
 코드에 대 한 자세한 설명을 참조 하세요 [HelloData에](../../../ado/guide/data/comments-on-hellodata.md)입니다.  
  
 ![HelloData VB 응용 프로그램에 대 한 Form1을 보여 줍니다](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
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
||캡션|데이터 검사|  
|명령 단추|이름|cmdEditData|  
||캡션|데이터 편집|  
|명령 단추|이름|cmdUpdateData|  
||캡션|업데이트 데이터|
