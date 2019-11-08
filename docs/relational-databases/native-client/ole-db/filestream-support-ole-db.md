---
title: FILESTREAM 지원 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3ff05424d9b8726f21c8c4aa2facd42b87961cc2
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73760881"
---
# <a name="filestream-support-ole-db"></a>FILESTREAM 지원(OLE DB)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0부터 OLE DB는 향상 된 FILESTREAM 기능을 지원 합니다. 이 기능에 대 한 자세한 내용은 [FILESTREAM 지원](../../../relational-databases/native-client/features/filestream-support.md)을 참조 하세요. 샘플은 [Filestream 및 OLE DB](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md)을 참조 하세요.  
  
 **Varbinary (max)** 값을 2gb 보다 크게 보내고 받으려면 응용 프로그램은 매개 변수 및 결과 바인딩에서 **DBTYPE_IUNKNOWN** 를 사용 합니다. 매개 변수의 경우 공급자는 ISequentialStream에 대해 IUnknown:: QueryInterface를 호출 하 고 ISequentialStream를 반환 하는 결과에 대해를 호출 해야 합니다.  
  
 OLE DB의 경우 ISequentialStream 값과 관련 된 검사가 완화 됩니다. **DBBINDING** 구조체에서 *wtype* 이 **DBTYPE_IUNKNOWN** 되 면 *dwpart* 에서 **DBPART_LENGTH** 생략 하거나 데이터의 길이를 설정 하 여 길이 검사를 비활성화할 수 있습니다 (데이터의 오프셋 *oblength* ). buffer)를 ~ 0으로 이렇게 하면 공급자는 값의 길이를 검사하지 않고 스트림을 통해 사용할 수 있는 모든 데이터를 요청하고 반환합니다. 이러한 변경 사항은 모든 LOB(큰 개체) 형식과 XML에 적용되지만, 이는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상의 서버에 연결된 경우에만 해당됩니다. 이 기능은 개발자에게 더 나은 융통성을 제공할 뿐만 아니라 기존 애플리케이션 및 하위 서버를 위한 일관성과 이전 버전과의 호환성을 유지할 수 있게 도와줍니다.  
  
 이 변경 내용은 데이터를 전송 하는 모든 인터페이스 (주로 IRowset:: GetData, ICommand:: Execute 및 IRowsetFastLoad:: InsertRow)에 영향을 줍니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client 프로그래밍](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
