---
title: 사용자에게 연결 정보 프롬프트 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b0f120a1076f14f5e67d506e52a446e0a3d4713
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282086"
---
# <a name="prompting-the-user-for-connection-information"></a>사용자에게 연결 정보 요청
응용 프로그램에서 **SQLConnect를** 사용하고 사용자 이름 및 암호와 같은 연결 정보를 사용자에게 표시해야 하는 경우 해당 응용 프로그램 자체를 수행해야 합니다. 이렇게 하면 응용 프로그램이 "모양과 느낌"을 제어할 수 있지만 응용 프로그램에 드라이버 관련 코드가 포함될 수 있습니다. 이 문제는 응용 프로그램이 사용자에게 드라이버 관련 연결 정보를 요청해야 할 때 발생합니다. 이렇게 하면 응용 프로그램을 작성할 때 존재하지 않는 드라이버를 포함하여 모든 드라이버와 함께 작동하도록 설계된 일반 응용 프로그램에 는 불가능한 상황이 있습니다.  
  
 **SQLDriverConnect는** 사용자에게 연결 정보를 묻는 메시지를 표시할 수 있습니다. 예를 들어 앞에서 언급한 사용자 지정 프로그램은 다음 연결 문자열을 **SQLDriverConnect에**전달할 수 있습니다.  
  
```  
DSN=XYZ Corp;  
```  
  
 그런 다음 드라이버는 다음 그림과 유사한 사용자 ID 및 암호를 묻는 대화 상자를 표시할 수 있습니다.  
  
 ![사용자 ID 및 암호를 묻는 대화 상자](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 드라이버가 연결 정보를 묻는 메시지가 표시될 수 있다는 것은 일반 및 수직 응용 프로그램에 특히 유용합니다. 이러한 응용 프로그램에는 드라이버 관련 정보가 포함되어서는 안 되며 필요한 정보에 대한 드라이버 프롬프트가 있으면 해당 정보가 응용 프로그램에서 제외됩니다. 이는 이전 두 예제에 의해 표시됩니다. 응용 프로그램이 드라이버에 데이터 원본 이름만 전달하면 응용 프로그램에 드라이버 관련 정보가 없으므로 특정 드라이버에 연결되지 않았습니다. 응용 프로그램이 드라이버에 전체 연결 문자열을 전달하면 해당 문자열을 해석할 수 있는 드라이버에 연결되었습니다.  
  
 일반 응용 프로그램은 이 작업을 한 단계 더 발전시키고 데이터 원본을 지정하지 않을 수도 있습니다. **SQLDriverConnect가** 빈 연결 문자열을 받으면 드라이버 관리자에 다음 대화 상자가 표시됩니다.  
  
 ![데이터 소스 선택 대화 상자](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 사용자가 데이터 원본을 선택하면 드라이버 관리자는 해당 데이터 원본을 지정하는 연결 문자열을 생성하여 드라이버에 전달합니다. 그런 다음 드라이버는 필요한 추가 정보를 사용자에게 표시할 수 있습니다.  
  
 드라이버가 사용자에게 프롬프트하는 조건은 *Driver완성* 플래그에 의해 제어됩니다. 프롬프트, 필요한 경우 프롬프트 또는 프롬프트하지 않는 옵션이 있습니다. 이 플래그에 대한 전체 설명은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명을 참조하십시오.
