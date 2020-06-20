---
title: ICommand(OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ICommand [SQL Server Native Client]
ms.assetid: 5e24b3a0-0658-44fc-b653-f4c52f9eb328
author: rothja
ms.author: jroth
ms.openlocfilehash: 03bdccc83a04078210f2283d0b330f237ed02979
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056176"
---
# <a name="icommand-ole-db"></a>ICommand(OLE DB)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client의 고유한 OLE DB 동작을 설명합니다.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 열 크기보다 큰 데이터를 삽입하면 일반적으로 오류가 발생합니다. 그러나 경우에 따라서는 S_OK가 반환되는 상황에서 *dwStatus* 가 DBSTATUS_S_TRUNCATED로 설정될 수도 있습니다. 이 문제는 대개 매개 변수를 사용하여 데이터를 삽입할 때 열이 너무 작아 데이터를 저장할 수 없고 `ICommandWithParameters::SetParameterInfo`가 호출되지 않은 경우에 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
