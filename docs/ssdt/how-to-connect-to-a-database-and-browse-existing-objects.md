---
title: '방법: 데이터베이스에 연결 및 기존 개체 찾아보기 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.connectionpicker.f1
ms.assetid: 9b331800-3806-4459-ac58-88cdc98124d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a0ac1a6b3363b826bab1530fb162ee6c0cb76c75
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47608099"
---
# <a name="how-to-connect-to-a-database-and-browse-existing-objects"></a>방법: 방법: 데이터베이스에 연결 및 기존 개체 찾아보기
데이터베이스 관리자 및 개발자가 수행하는 가장 일반적인 작업은 라이브 데이터베이스에 연결하고, 해당 스키마를 디자인하거나 찾아보고, 개체에 대해 쿼리하는 것입니다. 이제 Visual Studio의 SQL Server 개체 탐색기에는 연결된 모든 **SQL Server** 인스턴스와 해당 데이터베이스가 SSMS와 유사한 계층 구조로 그룹화되는 전용 SQL Server 노드가 포함되어 있습니다. 연결된 SQL Server 인스턴스는 실행 중인 SQL Server 2008과 같은 내부 인스턴스이거나 외부 SQL Azure 인스턴스일 수 있습니다.  
  
다음 절차에서는 AdventureWorks 예제 데이터베이스를 이미 설치했다고 가정합니다. [CodePlex](http://msftdbprodsamples.codeplex.com/)를 사용하여 다른 SQL Server 버전의 예제 데이터베이스를 찾아 설치합니다. 원하는 경우 단계에 따라 사용 중인 서버의 기존 데이터베이스를 사용할 수도 있습니다.  
  
### <a name="to-connect-to-a-database-instance"></a>데이터베이스 인스턴스에 연결하려면  
  
1.  Visual Studio에서 **SQL Server 개체 탐색기**가 열려 있는지 확인합니다. 열려 있지 않으면 **보기** 메뉴를 클릭하고 **SQL Server 개체 탐색기**를 선택합니다.  
  
2.  **SQL Server 개체 탐색기**에서 **SQL Server** 노드를 마우스 오른쪽 단추로 클릭하고 **SQL Server 추가**를 선택합니다.  
  
3.  **서버에 연결** 대화 상자에서 연결할 서버 인스턴스의 **서버 이름** 을 입력하고 **연결**을 클릭합니다.  
  
4.  **SQL Server 개체 탐색기**에서 서버 인스턴스 아래의 **데이터베이스** 노드를 확장합니다. 이 서버 인스턴스에 있는 모든 데이터베이스가 이 **데이터베이스** 노드 아래에 표시됩니다.  
  
5.  **AdventureWorks**(또는 다른 데이터베이스) 노드를 확장합니다. 모든 데이터베이스 엔터티가 SQL Server Management Studio와 비슷한 계층 구조로 구성되어 있는지 확인합니다.  
  
