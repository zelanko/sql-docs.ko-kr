---
title: 등록된 서버 정보 내보내기(SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.exportregisteredservers.f1
helpviewer_keywords:
- Registered Servers [SQL Server], exporting
- exporting registered server information
- transferring registered server information
ms.assetid: b65e168f-b6bf-489c-b8ad-3b8644acf0b6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9d1a853c5469fc30ef9545c0a062fdd1933f5c9b
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65104408"
---
# <a name="export-registered-server-information-sql-server-management-studio"></a>등록된 서버 정보 내보내기(SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 등록된 서버 정보를 저장하여 내보내고 그 정보를 다른 사용자나 서버로 배포하는 방법에 대해 설명합니다. 이러한 내보내기 기능을 사용하면 여러 대의 컴퓨터에서 일관된 사용자 인터페이스를 사용할 수 있습니다.  
  
 등록된 서버 파일을 내보냈다가 다시 가져오면 등록된 서버에 있는 동일한 서버로 여러 컴퓨터를 쉽게 구성할 수 있습니다. 이 작업은 여러 곳에 위치한 컴퓨터에서 다수의 서버를 관리할 때나 경험이 적은 사용자를 위해 기본 연결 설정을 구성하려는 경우에 유용합니다.  
  
> [!NOTE]  
>  SQL Server 인증을 사용하는 서버 등록은 사용자 단위로 암호를 저장합니다. 서버 등록을 내보냈다가 가져온 후 사용자는 처음으로 연결할 때 각 서버의 암호를 입력하여 등록된 서버 목록에 암호를 저장해야 합니다. Windows 인증을 통해 등록된 서버에는 이 작업이 필요하지 않습니다.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-export-registered-server-information"></a>등록된 서버 정보를 내보내려면  
  
1.  등록된 서버에서 서버 그룹을 마우스 오른쪽 단추로 클릭한 다음 **내보내기**를 클릭합니다.  
  
    > [!NOTE]  
    >  개별 서버, 등록된 모든 서버 트리 또는 등록된 서버 트리의 하위 집합을 내보낼 수 있습니다.  
  
2.  **등록된 서버 내보내기** 대화 상자에서 다음과 같이 선택합니다.  
  
     **서버 그룹**  
     내보낼 서버 그룹을 지정합니다. 등록된 모든 서버, 특정 서버 그룹에 속한 등록된 서버 또는 등록된 단일 서버를 내보내기 파일로 내보냅니다. 내보내기 기능은 재귀적입니다. 예를 들어 서버 그룹 A에는 서버 그룹 B가, 서버 그룹 B에는 서버 그룹 C와 D가 포함된 경우 서버 그룹 A를 내보내면 A, B, C, D의 모든 항목이 내보내집니다.  
  
     서버 그룹은 현재 등록된 서버 트리의 서버 그룹만 표시합니다.  
  
     **내보낼 파일**  
     입력란에 내보낼 파일 이름을 입력하거나 찾아보기 단추(**...**)를 사용하여 클라이언트 컴퓨터에서 내보낼 파일을 찾습니다. 기존 파일을 선택하면 등록된 서버 정보가 파일에 추가됩니다. .regsrvr 확장명을 사용합니다. 등록된 서버 정보를 다른 사용자나 컴퓨터도 사용할 수 있게 하려면 네트워크에 해당 파일을 저장하면 됩니다. 다른 사용자는 해당 파일에 액세스하여 등록된 서버 정보의 일부 또는 전체를 가져올 수 있습니다. 파일을 내보낼 때 기존 파일을 선택하면 파일 내용을 새 서버 등록 정보로 덮어씁니다.  
  
     **파일 내보내기에 사용자 이름 및 암호 포함 안 함**  
     파일을 내보낼 때 사용자 이름을 제외합니다.  
  
    > [!IMPORTANT]  
    >  내보낼 파일이 암호화되더라도 파일에 사용자 이름과 SQL Server 인증 암호가 포함되면 파일에 대한 액세스를 신중하게 제어해야 합니다. 따라서 사용자 이름과 암호는 기본적으로 내보낼 파일에서 제외됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [등록된 서버 정보 가져오기&#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md)   
 [새 등록된 서버 만들기&#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)  
  
  
