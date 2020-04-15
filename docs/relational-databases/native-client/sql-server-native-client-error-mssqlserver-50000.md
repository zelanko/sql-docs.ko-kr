---
title: MSSQLSERVER_50000 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c94c6ba66c7b943fa029bc1cb7e303cd946b0c4c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305357"
---
# <a name="sql-server-native-client-error-mssqlserver_50000"></a>SQL Server Native Client 오류 MSSQLSERVER_50000
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|제품 버전|11.0|  
|이벤트 ID|50000|  
|이벤트 원본|SETUP|  
|구성 요소|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client|  
|심볼 이름||  
|메시지 텍스트|'%.*ls' 파일을 읽는 동안 네트워크가 오류가 발생했습니다.|  
  
## <a name="explanation"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client가 이미 설치되어 있는 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 설치하거나 업데이트하려 했습니다. 기존 설치는 sqlncli.msi에서 이름이 바뀐 MSI 파일에서 설치되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
 이 오류를 해결하려면 기존의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 버전을 제거하십시오. 이 오류가 발생하지 않도록 하려면 sqlncli.msi로 이름이 지정되지 않은 MSI 파일에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 설치하지 마십시오.  
  
## <a name="internal-only"></a>내부 전용  
  
