---
title: 연결 정보에 대 한 사용자에 게 확인 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connecting to data source [ODBC], SqlConnect
- connecting to driver [ODBC], prompting user for information
- connecting to driver [ODBC], SQLConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLConnect function [ODBC], prompting user for connection information
- connecting to data source [ODBC], prompting user for information
- prompting user for connection information [ODBC]
- SQLDriverConnect function [ODBC], prompting user for connection information
ms.assetid: da98e9b9-a4ac-4a9d-bae6-e9252b1fe1e5
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 796713fb12fe2eb70a0e7630ec558a63d7cfec4d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="prompting-the-user-for-connection-information"></a>연결 정보에 대 한 사용자에 게 확인
응용 프로그램을 사용 하는 경우 **SQLConnect** 및 연결 정보를 묻는 메시지를 필요로 하는 사용자 이름과 암호 같은 해야 자체입니다. 응용 프로그램을 "디자인"을 제어할 수 있으며, 드라이버 관련 코드를 포함 하도록 응용 프로그램을 강제로 수 있습니다. 이 응용 프로그램 사용자에 게 드라이버 관련 연결 정보 해야 할 때 발생 합니다. 이 응용 프로그램을 작성할 때 존재 하지 않는 드라이버를 포함 하는 모든 드라이버와 함께 작동 하도록 설계 된 일반 응용 프로그램에 대 한는 불가능 한 상황을 표시 합니다.  
  
 **SQLDriverConnect** 사용자에 게 연결 정보를 표시할 수 있습니다. 예를 들어 앞에서 언급 한 사용자 지정 프로그램은 다음 연결 문자열을 전달 **SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 그런 다음 드라이버 사용자 Id, 다음 그림과 유사 하 게 암호를 묻는 대화 상자를 표시할 수 있습니다.  
  
 ![사용자 Id 및 암호를 묻는 대화 상자를](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 연결 정보에 대 한 드라이버를 표시할 수 있습니다 제네릭 및 세로 응용 프로그램에 특히 유용 합니다. 이러한 응용 프로그램에는 드라이버 관련 정보 없어야 하 고 응용 프로그램에서 해당 정보를 유지 하는 데 필요한 정보에 대 한 드라이버 프롬프트 필요 합니다. 이 앞의 두 예제도 표시 됩니다. 데이터 원본 이름을 드라이버에 전달 하는 응용 프로그램, 응용 프로그램 모든 드라이버 관련 정보가 포함 되어 있지 않으면와 특정 드라이버 하지 연결 따라서가 있습니다. 전체 연결 문자열을 드라이버에 전달 하는 응용 프로그램을이 해당 문자열을 해석할 수 있는 드라이버에 연결 되었습니다.  
  
 일반 응용 프로그램 추가이 한 단계를 수행할 수 있습니다 및 하더라도 데이터 원본을 지정 합니다. 때 **SQLDriverConnect** 다음 대화 상자에 빈 연결 문자열을 표시 되는 경우 드라이버 관리자를 받습니다.  
  
 ![데이터 원본 대화 상자 선택](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 사용자가 데이터 소스를 선택한 후 드라이버 관리자는 해당 데이터 원본을 지정 하는 연결 문자열을 생성 하 고 드라이버에 전달 합니다. 드라이버는 필요한 추가 정보에 대 한 사용자를 표시 한 다음 수 있습니다.  
  
 드라이버는 사용자를 요청 하는 조건에 의해 제어 됩니다는 *DriverCompletion* 플래그; 항상 확인 하 고, 필요에 따라 메시지를 표시 또는 확인 안 함 하는 옵션이 있습니다. 에 대 한 전체 설명은이 플래그를 참조 하십시오.는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명 합니다.
