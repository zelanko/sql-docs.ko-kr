---
title: 상태 표시줄(데이터베이스 엔진 쿼리 편집기) | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e7f2d6f4-bb94-4cf5-a096-c34397e679af
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 23a7477816a6529efceb99324edb2a5cdc8dc9c9
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43061625"
---
# <a name="status-bar-database-engine-query-editor"></a>상태 표시줄(데이터베이스 엔진 쿼리 편집기)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창에서 각 창이 연결되는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 나타내도록 상태 표시줄을 색으로 구분할 수 있습니다.  
  
1.  **시작하기 전에:**  [상태 표시줄 색](#StatusBarColors)  
  
2.  **개체 탐색기에서 서버 상태 색을 설정하려면:**  [개체 탐색기](#SetOEServerColor), [등록되 서버](#SetRegServerColor)  
  
3.  **상태 색을 사용하려면:**  [서버 색을 사용하여 쿼리 편집기 열기](#OpenServerColor), [상태 색을 지정하여 쿼리 편집기 열기](#OpenSpecColor)  
  
##  <a name="StatusBarColors"></a> 상태 표시줄 색  
 **개체 탐색기** 또는 **등록된 서버**에서 상태 표시줄 색을 특정 서버 노드에 연결할 수 있습니다. 색은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결된 서버 노드에 대해서만 지정할 수 있고 다른 SQL Server 기술에 대한 서버 노드에 대해서는 지정할 수 없습니다. 새 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창을 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결할 때마다 사용자 지정 상태 표시줄 색을 지정할 수도 있습니다. 그런 다음 서버 노드에 대해 정의된 상태 색을 사용하거나 해당 편집기 창에 고유한 색을 지정하여 쿼리 편집기 창을 열 수 있습니다.  
  
 개체 탐색기에서 서버 노드에 대한 사용자 지정 상태 표시줄 색을 설정하려면 연결할 때 색을 지정해야 합니다. 기존 서버 노드에 연결된 색을 변경하려면 연결을 끊었다가 다시 연결하여 새 색을 지정해야 합니다.  
  
##  <a name="SetOEServerColor"></a> 개체 탐색기에서 서버에 대한 상태 색 설정  
 **개체 탐색기에서 서버 상태 색을 설정하려면**  
  
1.  **개체 탐색기**에서 **연결** 단추를 선택한 다음 **데이터베이스 엔진...** 을 선택합니다.  
  
2.  **서버에 연결** 대화 상자에서 **옵션 >>** 을 선택합니다.  
  
3.  **사용자 지정 색 사용** 확인란을 선택합니다.  
  
4.  색을 선택하려면 **선택…** 단추를 선택합니다.  
  
5.  기본 색 또는 사용자 지정 색 중 하나를 선택하고 확인을 선택합니다.  
  
6.  나머지 연결 정보를 입력한 다음 **연결** 단추를 선택합니다.  
  
##  <a name="SetRegServerColor"></a> 등록된 서버에 대한 상태 색 설정  
 **등록된 서버에 대한 서버 색을 설정하려면**  
  
1.  **등록된 서버**에서 서버 노드를 마우스 오른쪽 단추로 클릭한 다음 **속성...** 을 선택합니다.  
  
2.  **서버 등록 속성 편집** 대화 상자에서 **연결 속성** 탭을 선택합니다.  
  
3.  **사용자 지정 색 사용** 확인란을 선택합니다.  
  
4.  색을 선택하려면 **선택…** 단추를 선택합니다.  
  
5.  기본 색 또는 사용자 지정 색 중 하나를 선택하고 확인을 선택합니다.  
  
6.  **서버 등록 속성 편집** 대화 상자에서 **저장** 단추를 선택합니다.  
  
##  <a name="OpenServerColor"></a> 서버 색을 사용하여 편집기 열기  
 **서버 색을 사용하여 편집기 창을 열려면**  
  
-   **개체 탐색기** 또는 **등록된 서버**에서 서버 노드를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.  
  
-   또는 서버 노드를 강조 표시한 다음 **새 쿼리** 도구 모음 단추를 선택합니다.  
  
-   편집기 창의 상태 표시줄에서 연결된 서버에 대해 정의된 색을 사용합니다.  
  
##  <a name="OpenSpecColor"></a> 상태 색을 지정하여 편집기 열기  
 **상태 색을 지정하여 편집기 창을 열려면**  
  
-   **파일** 메뉴를 열고 **새로 만들기**를 선택한 다음 **데이터베이스 엔진 쿼리**를 선택합니다.  
  
-   **서버에 연결** 대화 상자에서 **옵션 >>** 을 선택합니다.  
  
-   **사용자 지정 색 사용** 확인란을 선택합니다.  
  
-   색을 선택하려면 **선택…** 단추를 선택합니다.  
  
-   기본 색 또는 사용자 지정 색 중 하나를 선택하고 확인을 선택합니다.  
  
-   나머지 연결 정보를 입력한 다음 **연결** 단추를 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [쿼리 및 텍스트 편집기&#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
