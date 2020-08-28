---
description: 'HelloData: 간단한 ADO 애플리케이션'
title: 'HelloData: 간단한 ADO 응용 프로그램 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
author: rothja
ms.author: jroth
ms.openlocfilehash: bec2b55f7daee865489c3f32e1ee70e53b9102a6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980634"
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData: 간단한 ADO 애플리케이션
이 간단한 응용 프로그램은 데이터 가져오기, 검사, 편집 및 업데이트의 네 가지 주요 ADO 작업을 각각 단계별로 안내 합니다. 이러한 작업은 Microsoft® SQL Server에 포함 된 Northwind 샘플 데이터베이스에 대해 수행 됩니다. ADO의 기본 사항에 집중 하 고 코드의 혼란을 방지 하기 위해 예제에서 오류 처리는 최소화 됩니다.  
  
### <a name="to-run-hellodata"></a>HelloData를 실행 하려면  
  
1.  ADO 라이브러리를 참조 하는 새 표준 EXE Visual Basic 프로젝트를 만듭니다. 자세한 내용은 [ADO 라이브러리 참조](../referencing-the-ado-libraries.md)를 참조 하세요.  
  
2.  **이름** 및 **캡션** 속성을이 항목의 끝에 있는 표에 표시 된 값으로 설정 하 여 폼의 맨 위에 4 개의 명령 단추를 만듭니다.  
  
3.  단추 아래에 **Microsoft DataGrid 컨트롤** (Msdatgrd.ocx)을 추가 합니다. Msdatgrd .ocx 파일은 Visual Basic 포함 되어 있으며, \windows\system32 또는 \winnt\system32 디렉터리에 있습니다. DataGrid 컨트롤을 Visual Basic 도구 상자 창에 추가 하려면 **프로젝트** 메뉴에서 **구성 요소 ...** 를 선택 합니다. 그런 다음 "Microsoft DataGrid 컨트롤 6.0 (SP3) (OLEDB)" 옆의 상자를 선택 하 고 **확인**을 클릭 합니다. 프로젝트에 컨트롤을 추가 하려면 도구 상자에서 DataGrid 컨트롤을 Visual Basic 폼으로 끌어 옵니다.  
  
4.  표 아래의 폼에 **텍스트 상자** 를 만들고 테이블에 표시 된 대로 속성을 설정 합니다. 완료 되 면 폼은 다음 그림과 유사 합니다.  
  
5.  마지막으로 [HelloData code](./hellodata-code.md)에 나열 된 코드를 복사 하 여 폼의 코드 편집기 창에 붙여넣습니다. **F5** 키를 눌러 코드를 실행 합니다.  
  
> [!NOTE]
>  다음 예에서는 가이드 전체에서 "123aBc" 암호를 사용 하는 사용자 id "MyId"를 사용 하 여 서버에 대해 인증 합니다. 이러한 값은 서버에 대 한 유효한 로그온 자격 증명으로 대체 해야 합니다. 또한 "MySQLServer" 값을 서버의 이름으로 대체 합니다.  
  
 코드에 대 한 자세한 설명은 [HelloData의 주석](./comments-on-hellodata.md)을 참조 하세요.  
  
 ![HelloData VB 응용 프로그램의 From1 표시](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|컨트롤 종류|속성|값|  
|------------------|--------------|-----------|  
|Form|Name|Form1|  
||높이|6500|  
||너비|6500|  
|MS DataGrid|Name|grdDisplay1|  
|TextBox|Name|txtDisplay1|  
||여러 줄|true|  
|명령 단추|Name|cmdGetData|  
||캡션|Get Data|  
|명령 단추|Name|cmdExamineData|  
||캡션|데이터 검사|  
|명령 단추|Name|cmdEditData|  
||캡션| 데이터 편집|  
|명령 단추|Name|cmdUpdateData|  
||캡션|업데이트 데이터|