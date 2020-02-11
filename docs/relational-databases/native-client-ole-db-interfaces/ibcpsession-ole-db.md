---
title: IBCPSession (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IBCPSession interface
ms.assetid: 00d0311f-8b71-4ad6-824d-0e89119347a3
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f3ea8d1e52ba5fc4d34f5bee1c728ff7ca3db2d7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73789582"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  
  **IBCPSession** 인터페이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 파일 기반 대량 복사 작업에 대한 지원을 노출합니다. 
  **IBCPSession** 인터페이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에서 세션과 같은 수준에 노출됩니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에서 데이터 원본 개체는 세션 개체에 대한 팩터리이고 대량 복사 작업은 연결 속성 SSPROP_ENABLEBULKCOPY에 지정됩니다. 또한 SSPROP_ENABLEFASTLOAD 속성을 true로 설정해야 합니다.  
  
 그런 다음 **IDBCreateSession::CreateSession** 메서드를 호출하면 **BulkCopySession** 개체가 생성됩니다. 그러면 **IBCPSession** 개체를 통해 노출되는 모든 파일 기반 대량 복사 메서드를 이 **IBCPSession** 개체의 **IBCPSession** 인터페이스에서 거의 유사한 서명을 사용하여 호출할 수 있습니다.  
  
> [!NOTE]  
>  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) 인터페이스를 통해 메모리 기반 대량 복사 작업을 지원합니다.  
  
 대량 복사 작업에 Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB 공급자를 사용 하는 방법에 대 한 자세한 내용은 [대량 복사 작업 수행](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)을 참조 하세요.  
  
 **IBCPSession** 인터페이스를 사용 하는 방법을 보여 주는 샘플은 [IBCPSession:: bcpdone &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|방법|Description|  
|------------|-----------------|  
|[IBCPSession:: BCPColFmt &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)|프로그램 변수와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열 간의 바인딩을 만듭니다.|  
|[IBCPSession:: BCPColumns &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 열에 바인딩될 필드의 개수를 설정합니다.|  
|[IBCPSession:: BCPControl &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)|대량 복사 작업에 대한 옵션을 설정합니다.|  
|[IBCPSession:: BCPDone &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 보낼 나머지 행을 커밋합니다.|  
|[IBCPSession:: BCPExec &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)|대량 복사 작업을 수행합니다.|  
|[IBCPSession:: BCPInit &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)|대량 복사 구조를 초기화하고, 일부 오류 검사를 수행하고, 데이터 및 서식 파일 이름이 올바른지 확인한 다음 파일을 엽니다.|  
|[IBCPSession:: BCPReadFmt &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)|서식 파일에서 각 열의 서식 정보를 읽습니다.|  
|[IBCPSession:: BCPWriteFmt &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)|각 열에 대한 서식 정보를 서식 파일에 기록합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스 &#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
