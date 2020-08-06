---
title: UDT 公用程式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 9e915268-9628-445b-81c2-b0ebd11e891e
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 7b2431db6b2ac915a895ed962dbf372ad41d849f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87701707"
---
# <a name="udt-utilities"></a><span data-ttu-id="c99e7-102">UDT 公用程式</span><span class="sxs-lookup"><span data-stu-id="c99e7-102">UDT Utilities</span></span>
  <span data-ttu-id="c99e7-103">這個「UDT 公用程式」範例包含數個公用程式函數。</span><span class="sxs-lookup"><span data-stu-id="c99e7-103">The UDT Utilities sample contains a number of utility functions.</span></span> <span data-ttu-id="c99e7-104">這些函數包括：將組件中繼資料公開至 Transact-SQL 的函數、將組件中的類型以資料表格式傳回的範例資料流資料表值函式，以及傳回使用者定義資料類型中之欄位、方法和屬性的函數。</span><span class="sxs-lookup"><span data-stu-id="c99e7-104">These include functions to expose assembly metadata to Transact-SQL, sample streaming table-valued functions to return the types in an assembly as a table, and functions to return the fields, methods, and properties in a user-defined data type.</span></span> <span data-ttu-id="c99e7-105">示範的技術包括資料流資料表值函式、.NET Framework 反映 API，以及 Transact-SQL 之資料表值函式的引動過程。</span><span class="sxs-lookup"><span data-stu-id="c99e7-105">Technologies that are demonstrated include streaming table-valued functions, .NET Framework reflection APIs, and invocation of table-valued functions from Transact-SQL.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="c99e7-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c99e7-106">Prerequisites</span></span>  
 <span data-ttu-id="c99e7-107">若要建立並執行這個專案，您必須安裝下列軟體：</span><span class="sxs-lookup"><span data-stu-id="c99e7-107">To create and run this project the following the following software must be installed:</span></span>  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="c99e7-108">或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express。</span><span class="sxs-lookup"><span data-stu-id="c99e7-108">or [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express.</span></span> <span data-ttu-id="c99e7-109">您可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 文件集和範例[網站](https://www.microsoft.com/sql-server/sql-server-editions-express)免費取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express</span><span class="sxs-lookup"><span data-stu-id="c99e7-109">You can obtain [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express free of charge from the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express Documentation and Samples [Web site](https://www.microsoft.com/sql-server/sql-server-editions-express)</span></span>  
  
-   <span data-ttu-id="c99e7-110">[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]可在 Codeplex[網站](https://go.microsoft.com/fwlink/?linkid=62796)取得的資料庫</span><span class="sxs-lookup"><span data-stu-id="c99e7-110">The [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] database that is available at the Codeplex [Web site](https://go.microsoft.com/fwlink/?linkid=62796)</span></span>  
  
-   <span data-ttu-id="c99e7-111">.NET Framework SDK 2.0 或更新版本或是 Microsoft Visual Studio 2005 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c99e7-111">.NET Framework SDK 2.0 or later or Microsoft Visual Studio 2005 or later.</span></span> <span data-ttu-id="c99e7-112">您可以免費取得 .NET Framework SDK。</span><span class="sxs-lookup"><span data-stu-id="c99e7-112">You can obtain .NET Framework SDK free of charge.</span></span>  
  
-   <span data-ttu-id="c99e7-113">此外，您也必須符合下列條件：</span><span class="sxs-lookup"><span data-stu-id="c99e7-113">In addition, the following conditions must be met:</span></span>  
  
-   <span data-ttu-id="c99e7-114">您所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體必須啟用 CLR 整合。</span><span class="sxs-lookup"><span data-stu-id="c99e7-114">The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance you are using must have CLR integration enabled.</span></span>  
  
-   <span data-ttu-id="c99e7-115">若要啟用 CLR 整合，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c99e7-115">In order to enable CLR integration, perform the following steps:</span></span>  
  
    #### <a name="enabling-clr-integration"></a><span data-ttu-id="c99e7-116">啟用 CLR 整合</span><span class="sxs-lookup"><span data-stu-id="c99e7-116">Enabling CLR Integration</span></span>  
  
    -   <span data-ttu-id="c99e7-117">執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令：</span><span class="sxs-lookup"><span data-stu-id="c99e7-117">Execute the following [!INCLUDE[tsql](../../includes/tsql-md.md)] commands:</span></span>  
  
     `sp_configure 'clr enabled', 1;`  
  
     `GO`  
  
     `RECONFIGURE;`  
  
     `GO`  
  
    > [!NOTE]  
    >  <span data-ttu-id="c99e7-118">若要啟用 CLR 整合，您必須擁有 `ALTER SETTINGS` 伺服器層級權限，此權限是由系統管理員 (`sysadmin`) 和伺服器管理員 (`serveradmin`) 固定伺服器角色的成員以隱含方式持有。</span><span class="sxs-lookup"><span data-stu-id="c99e7-118">To enable CLR, you must have `ALTER SETTINGS` server level permission, which is implicitly held by members of the `sysadmin` and `serveradmin` fixed server roles.</span></span>  
  
-   <span data-ttu-id="c99e7-119">[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫必須安裝在您所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上。</span><span class="sxs-lookup"><span data-stu-id="c99e7-119">The [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] database must be installed on the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance you are using.</span></span>  
  
-   <span data-ttu-id="c99e7-120">如果您不是正在使用之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的管理員，則必須讓管理員授與您 **CreateAssembly** 權限來完成安裝。</span><span class="sxs-lookup"><span data-stu-id="c99e7-120">If you are not an administrator for the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance you are using, you must have an administrator grant you **CreateAssembly**  permission to complete the installation.</span></span>  
  
## <a name="building-the-sample"></a><span data-ttu-id="c99e7-121">建立範例</span><span class="sxs-lookup"><span data-stu-id="c99e7-121">Building the Sample</span></span>  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a><span data-ttu-id="c99e7-122">使用下列指示來建立並執行範例：</span><span class="sxs-lookup"><span data-stu-id="c99e7-122">Create and run the sample by using the following instructions:</span></span>  
  
1.  <span data-ttu-id="c99e7-123">開啟 Visual Studio 或 .NET Framework 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="c99e7-123">Open a Visual Studio or .NET Framework command prompt.</span></span>  
  
2.  <span data-ttu-id="c99e7-124">必要時，請建立範例的目錄。</span><span class="sxs-lookup"><span data-stu-id="c99e7-124">If necessary, create a directory for your sample.</span></span> <span data-ttu-id="c99e7-125">在此範例中，我們將使用 C:\MySample。</span><span class="sxs-lookup"><span data-stu-id="c99e7-125">For this example, we will use C:\MySample.</span></span>  
  
3.  <span data-ttu-id="c99e7-126">因為此範例需要已簽署的組件，所以請輸入下列命令，藉以建立非對稱金鑰：</span><span class="sxs-lookup"><span data-stu-id="c99e7-126">Since this example requires a signed assembly, create an asymmetric key by typing the command:</span></span>  
  
     `sn -k SampleKey.snk`  
  
4.  <span data-ttu-id="c99e7-127">根據您選擇的語言，在命令列提示字元中執行下列其中一段程式碼，藉以編譯範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="c99e7-127">Compile the sample code from the command line prompt by executing one of the following, depending on your choice of language.</span></span>  
  
    -   `Vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /keyfile:Key.snk /out:UDTUtilities.dll  /target:library AssemblyBrowser.vb`  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.XML.dll /keyfile:Key.snk /out:UDTUtilities.dll /target:library AssemblyBrowser.cs`  
  
5.  <span data-ttu-id="c99e7-128">將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安裝程式碼複製到檔案中，並將它儲存成範例目錄中的 `Install.sql`。</span><span class="sxs-lookup"><span data-stu-id="c99e7-128">Copy the [!INCLUDE[tsql](../../includes/tsql-md.md)] installation code into a file and save it as `Install.sql` in the sample directory.</span></span>  
  
6.  <span data-ttu-id="c99e7-129">部署組件和預存程序，方法是執行</span><span class="sxs-lookup"><span data-stu-id="c99e7-129">Deploy the assembly and stored procedure by executing</span></span>  
  
    -   `sqlcmd -E -I -i install.sql -v root = "C:\MySample\"`  
  
7.  <span data-ttu-id="c99e7-130">將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 測試命令腳本複製到檔案中，並將它儲存成 `test.sql` 範例目錄中的。</span><span class="sxs-lookup"><span data-stu-id="c99e7-130">Copy [!INCLUDE[tsql](../../includes/tsql-md.md)] test command script into a file and save it as `test.sql` in the sample directory.</span></span>  
  
8.  <span data-ttu-id="c99e7-131">使用下列命令來執行測試指令碼</span><span class="sxs-lookup"><span data-stu-id="c99e7-131">Execute the test script with the following command</span></span>  
  
    -   `sqlcmd -E -I -i test.sql`  
  
9. <span data-ttu-id="c99e7-132">將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 清除指令碼複製到檔案中，並將它儲存成範例目錄中的 `cleanup.sql`。</span><span class="sxs-lookup"><span data-stu-id="c99e7-132">Copy the [!INCLUDE[tsql](../../includes/tsql-md.md)] cleanup script into a file and save it as `cleanup.sql` in the sample directory.</span></span>  
  
10. <span data-ttu-id="c99e7-133">使用下列命令來執行指令碼</span><span class="sxs-lookup"><span data-stu-id="c99e7-133">Execute the script with the  following command</span></span>  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a><span data-ttu-id="c99e7-134">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="c99e7-134">Sample Code</span></span>  
 <span data-ttu-id="c99e7-135">下面是此範例的程式碼清單。</span><span class="sxs-lookup"><span data-stu-id="c99e7-135">The following are the code listings for this sample.</span></span>  
  
 <span data-ttu-id="c99e7-136">C#</span><span class="sxs-lookup"><span data-stu-id="c99e7-136">C#</span></span>  
  
```  
using System;  
using System.Collections;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using System.Reflection;  
using Microsoft.SqlServer.Server;  
using System.Globalization;  
using System.Text;  
using System.Data.SqlClient;  
    /// <summary>  
    /// AssemblyBrowser is a simple utility for composing sql queries over   
    /// assembly metadata. It uses a table-valued-function to return  
    /// a table to SqlServer.  
    /// </summary>  
    public sealed class AssemblyBrowser  
    {  
        /// <summary>  
        /// Get the types in the assembly, as a table  
        /// </summary>  
        /// <param name="name"></param>  
        /// <returns></returns>  
        [SqlFunction(FillRowMethodName = "FillTypeRow")]  
        public static IEnumerable GetTypes(String name)  
        {  
            IEnumerable e;  
  
            try  
            {  
                Assembly a = Assembly.Load(name);  
                if (a == null)  
                    e = new Type[0];  
                else  
                    e = a.GetTypes();  
            }  
  
            catch (ReflectionTypeLoadException te)  
            {  
                //could not load some of the types, just return the types that you could load  
                e = te.Types;  
            }  
  
            if (e == null) e = new Type[0];  
            return e;  
  
        }  
  
        /// <summary>  
        /// Get the schema of the table  
        /// </summary>  
        /// <returns></returns>  
  
        public static void FillTypeRow(object metaData, out string fullName, out string baseTypeName,  
            out bool isValueType, out int numFields, out bool isSerializable,  
            out bool isISerializable, out bool isLayoutSequential, out string namespaceValue,  
            out bool isPublic, out bool isSealed, out string assemblyName)  
        {  
            Type type = (Type)metaData;  
            fullName = type.FullName;  
            baseTypeName = (type.BaseType == null) ? "" : type.BaseType.FullName;  
            isValueType = type.IsValueType;  
            FieldInfo[] fields = type.GetFields(BindingFlags.Instance | BindingFlags.Public);  
            numFields = (fields == null) ? 0 : fields.Length;  
            isSerializable = type.IsSerializable;  
            isISerializable = typeof(System.Runtime.Serialization.ISerializable).IsAssignableFrom(type);  
            isLayoutSequential = type.IsLayoutSequential;  
            namespaceValue = type.Namespace;  
            isPublic = type.IsPublic;  
            isSealed = type.IsSealed;  
            Assembly a = type.Assembly;  
            assemblyName = (a == null) ? "null" : a.GetName().Name;  
        }  
  
        internal static Assembly GetAssembly(string name)  
        {  
            try  
            {  
                return Assembly.Load(name);  
            }  
            catch (System.IO.FileNotFoundException)  
            {  
                return null;  
            }  
        }  
  
        private AssemblyBrowser() { }  
        [SqlFunction(FillRowMethodName = "FillAssemblyRow")]  
        public static IEnumerable GetLoadedAssemblies()  
        {  
            IEnumerable e = AppDomain.CurrentDomain.GetAssemblies();  
            //Microsoft.SqlServer.Server.SqlMetaData[] schemas  
            //    = new Microsoft.SqlServer.Server.SqlMetaData[] {  
            //    new Microsoft.SqlServer.Server.SqlMetaData("FullName", SqlDbType.NVarChar, 256)  
            //};  
  
            return e;  
        }  
  
        private static void FillAssemblyRow(object source, out string fullName)  
        {  
            fullName = ((Assembly)source).FullName;  
        }  
    }  
  
    [Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute(Microsoft.SqlServer.Server.Format.Native)]  
    [Serializable]  
    public struct SimpleUdt : INullable  
    {  
        #region udt contract  
        public override string ToString()  
        {  
            return base.ToString();  
        }  
  
        public bool IsNull  
        {  
            get  
            {  
                return this._value.IsNull;  
            }  
        }  
  
        public static SimpleUdt Null  
        {  
            get  
            {  
                SimpleUdt h = new SimpleUdt();  
  
                return h;  
            }  
        }  
  
        public static SimpleUdt Parse(SqlString sqlString)  
        {  
            if (sqlString.IsNull)  
                return Null;  
  
            SimpleUdt u = new SimpleUdt();  
  
            u.Value = new SqlInt32(int.Parse(sqlString.Value,  
                CultureInfo.InvariantCulture));  
  
            return u;  
        }  
        #endregion  
  
        #region implementation  
        private SqlInt32 _value;  
  
        private SqlInt32 _examplePublicField;  
  
        public SqlInt32 ExamplePublicField  
        {  
            get  
            {  
                return this._examplePublicField;  
            }  
            set  
            {  
                this._examplePublicField = value;  
            }  
        }  
  
        public SqlInt32 Value  
        {  
            get  
            {  
                return this._value;  
            }  
            set  
            {  
                this._value = value;  
            }  
        }  
  
        [Microsoft.SqlServer.Server.SqlMethod(IsDeterministic = true)]  
        public SqlInt32 ReturnValue()  
        {  
            return this._value;  
        }  
  
        #endregion  
    }  
    /// <summary>  
    /// Utility Udt functions  
    /// </summary>  
    public sealed class UdtServices  
    {  
  
        #region udt fields  
        /// <summary>  
        /// Get the fields in the UDT callable from tsql, as a table  
        /// </summary>  
        /// <param name="udtName"></param>  
        /// <returns></returns>  
        [SqlFunctionAttribute(FillRowMethodName = "FillFieldRow")]  
        public static IEnumerable GetUdtFields(string udtName)  
        {  
            return GetSqlFields(GetUdt(udtName));  
        }  
  
        public static void FillFieldRow(object fieldMetadata, out string name, out string type)  
        {  
            FieldInfo fieldInformation = (FieldInfo)fieldMetadata;  
            name = fieldInformation.Name;  
            type = fieldInformation.FieldType.Name;  
        }  
  
        #endregion  
  
        #region udt properties  
        /// <summary>  
        /// Get the properties defined in a particular UDT  
        /// </summary>  
        /// <param name="udtName"></param>  
        /// <returns></returns>  
        [SqlFunctionAttribute(FillRowMethodName = "FillPropertyRow")]  
        public static IEnumerable GetUdtProperties(string udtName)  
        {  
            return GetSqlProperties(GetUdt(udtName));  
        }  
  
        public static void FillPropertyRow(object propertyMetadata, out string name, out string type, out string routineProperties)  
        {  
            PropertyInfo propertyInformation = (PropertyInfo)propertyMetadata;  
            name = propertyInformation.Name;  
            type = propertyInformation.PropertyType.Name;  
            MethodInfo methodInformation = propertyInformation.GetGetMethod();  
            object[] attrs = methodInformation.GetCustomAttributes(  
                typeof(Microsoft.SqlServer.Server.SqlMethodAttribute), true);  
  
            if (attrs != null && attrs.Length == 1)  
            {  
                Microsoft.SqlServer.Server.SqlMethodAttribute attr  
                    = (Microsoft.SqlServer.Server.SqlMethodAttribute)attrs[0];  
  
                routineProperties = GetRoutineProperties(attr);  
            }  
            else  
                routineProperties = "";  
        }  
  
        #endregion  
  
        #region udt methods  
        /// <summary>  
        /// Get the methods on the UDT callable from tsql, as a table  
        /// </summary>  
        /// <param name="udtName"></param>  
        /// <returns></returns>  
        [SqlFunctionAttribute(FillRowMethodName = "FillMethodRow")]  
        public static IEnumerable GetUdtMethods(string udtName)  
        {  
            return GetSqlMethods(GetUdt(udtName));  
        }  
  
        public static void FillMethodRow(object methodMetadata, out string name,  
            out string parameters, out string returnType, out string routineProperties)  
        {  
            MethodInfo methodInformation = (MethodInfo)methodMetadata;  
            name = methodInformation.Name;  
            StringBuilder sb = new StringBuilder("(");  
            bool first = true;  
  
            foreach (ParameterInfo pi in methodInformation.GetParameters())  
            {  
                if (first)  
                    first = false;  
                else  
                    sb.Append(", ");  
  
                sb.Append(pi.Name).Append(" ").Append(pi.ParameterType.Name);  
            }  
  
            sb.Append(")");  
  
            parameters = sb.ToString();  
            returnType = methodInformation.ReturnType.Name;  
  
            object[] attrs = methodInformation.GetCustomAttributes(  
                typeof(Microsoft.SqlServer.Server.SqlMethodAttribute), true);  
  
            if (attrs != null && attrs.Length == 1)  
            {  
                Microsoft.SqlServer.Server.SqlMethodAttribute attr  
                    = (Microsoft.SqlServer.Server.SqlMethodAttribute)attrs[0];  
  
                routineProperties = GetRoutineProperties(attr);  
            }  
            else  
                routineProperties = "";  
  
        }  
  
        #endregion  
  
        #region internal utility functions  
  
        private UdtServices()  
        {  
        }  
  
        /// <summary>  
        /// Utility function to get the string representation of  
        /// routine properties on a type  
        /// </summary>  
        /// <param name="attr"></param>  
        /// <returns></returns>  
        private static string GetRoutineProperties(Microsoft.SqlServer.Server.SqlMethodAttribute attr)  
        {  
            StringBuilder sb = new StringBuilder();  
            if (attr.OnNullCall)  
                sb.Append("on_null_call ");  
  
            if (attr.IsMutator)  
                sb.Append("mutator ");  
  
            if (attr.IsDeterministic)  
                sb.Append("deterministic ");  
  
            if (attr.IsPrecise)  
                sb.Append("precise ");  
  
            if (attr.DataAccess != Microsoft.SqlServer.Server.DataAccessKind.None)  
                sb.Append("data_access " + Enum.GetName(  
                    typeof(Microsoft.SqlServer.Server.DataAccessKind), attr.DataAccess));  
  
            return sb.ToString();  
        }  
  
        /// <summary>  
        /// Is this a valid parameter type that can be accessible from tsql  
        /// </summary>  
        /// <param name="t"></param>  
        /// <returns></returns>  
        private static bool IsSqlParameterType(Type t)  
        {  
            if (validParameterTypes.ContainsKey(t))  
                return true;  
  
            if (t.FullName.StartsWith("System.Data.SqlTypes"))  
                return true;  
  
            if (t.GetCustomAttributes(  
                typeof(Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute),  
                true).Length == 1)  
                return true;  
  
            return false;  
        }  
  
        /// <summary>  
        /// Is the field type valid?  
        /// </summary>  
        /// <param name="f"></param>  
        /// <param name="declaringType"></param>  
        /// <returns></returns>  
        private static bool IsSqlField(FieldInfo f, Type declaringType)  
        {  
            if (f.DeclaringType != declaringType)  
                return false;  
  
            return IsSqlParameterType(f.FieldType);  
        }  
  
        /// <summary>  
        /// Is the property valid to be called from tsql?  
        /// </summary>  
        /// <param name="f"></param>  
        /// <param name="declaringType"></param>  
        /// <returns></returns>  
        private static bool IsSqlProperty(PropertyInfo f, Type declaringType)  
        {  
            if (f.DeclaringType != declaringType)  
                return false;  
  
            return IsSqlParameterType(f.PropertyType);  
        }  
  
        /// <summary>  
        /// Is the method valid to be called from tsql?  
        /// </summary>  
        /// <param name="m"></param>  
        /// <param name="declaringType"></param>  
        /// <returns></returns>  
        private static bool IsSqlMethod(MethodInfo m, Type declaringType)  
        {  
            if (m.DeclaringType != declaringType)  
                return false;  
  
            foreach (ParameterInfo info in m.GetParameters())  
            {  
                if (!IsSqlParameterType(info.ParameterType))  
                    return false;  
            }  
  
            return IsSqlParameterType(m.ReturnType);  
        }  
  
        /// <summary>  
        /// Get the udt specified by the clr type name.  
        /// </summary>  
        /// <param name="udtName"></param>  
        /// <returns></returns>  
        private static Type GetUdt(string udtName)  
        {  
            return Type.GetType(udtName, true);  
        }  
  
        /// <summary>  
        /// Get the methods on a type  
        /// </summary>  
        /// <param name="t"></param>  
        /// <returns></returns>  
        private static ICollection GetSqlMethods(Type t)  
        {  
            MethodInfo[] methods = t.GetMethods(BindingFlags.Instance | BindingFlags.Public | BindingFlags.DeclaredOnly);  
            ArrayList temp = new ArrayList();  
  
            foreach (MethodInfo info in methods)  
            {  
                if (IsSqlMethod(info, t))  
                    temp.Add(info);  
            }  
  
            return temp;  
        }  
  
        /// <summary>  
        /// get the properties on a type  
        /// </summary>  
        /// <param name="t"></param>  
        /// <returns></returns>  
        private static ICollection GetSqlProperties(Type t)  
        {  
            PropertyInfo[] props = t.GetProperties(BindingFlags.Instance | BindingFlags.Public | BindingFlags.DeclaredOnly);  
            ArrayList temp = new ArrayList();  
  
            foreach (PropertyInfo info in props)  
            {  
                if (IsSqlProperty(info, t))  
                    temp.Add(info);  
            }  
  
            return temp;  
        }  
  
        /// <summary>  
        /// get the fields on a type  
        /// </summary>  
        /// <param name="t"></param>  
        /// <returns></returns>  
        private static ICollection GetSqlFields(Type t)  
        {  
            FieldInfo[] fields = t.GetFields(BindingFlags.Instance | BindingFlags.Public | BindingFlags.DeclaredOnly);  
            ArrayList temp = new ArrayList();  
  
            foreach (FieldInfo info in fields)  
            {  
                if (IsSqlField(info, t))  
                    temp.Add(info);  
            }  
  
            return temp;  
        }  
  
        /// <summary>  
        /// readonly static used to cache frequently used information  
        /// </summary>  
        private static readonly Hashtable validParameterTypes = GetValidParameterTypes();  
  
        /// <summary>  
        /// initialize the cached mapping of valid parameter types  
        /// </summary>  
        private static Hashtable GetValidParameterTypes()  
        {  
            Hashtable validTypes = new Hashtable();  
            validTypes[typeof(bool)] = true;  
            validTypes[typeof(byte)] = true;  
            validTypes[typeof(short)] = true;  
            validTypes[typeof(char)] = true;  
            validTypes[typeof(int)] = true;  
            validTypes[typeof(float)] = true;  
            validTypes[typeof(long)] = true;  
            validTypes[typeof(double)] = true;  
            validTypes[typeof(string)] = true;  
            validTypes[typeof(Guid)] = true;  
  
            return validTypes;  
        }  
        #endregion  
  
        #region public utility functions  
        [Microsoft.SqlServer.Server.SqlFunction(DataAccess = Microsoft.SqlServer.Server.DataAccessKind.Read)]  
        public static string GetFullAssemblyName(string sqlName)  
        {  
            using (System.Data.SqlClient.SqlConnection conn = new SqlConnection("context connection=true"))  
            {  
                SqlCommand cmd = conn.CreateCommand();  
                cmd.CommandText = @"SELECT @sqlName, "  
                + @"assemblyproperty(@sqlName, 'VersionMajor'), "  
                + @"assemblyproperty(@sqlName, 'VersionMinor'), "  
                + @"assemblyproperty(@sqlName, 'VersionBuild'), "  
                + @"assemblyproperty(@sqlName, 'VersionRevision'), "  
                + @"assemblyproperty(@sqlName, 'CultureInfo'), "  
                + @"assemblyproperty(@sqlName, 'PublicKey'), "  
                + @"assemblyproperty(@sqlName, 'Architecture');";  
  
                cmd.Parameters.AddWithValue("@sqlName", sqlName);  
  
                conn.Open();  
  
                SqlDataReader rdr = cmd.ExecuteReader();  
  
                try  
                {  
                    if (!rdr.Read())  
                        throw new ArgumentException(string.Format(  
                            CultureInfo.InvariantCulture,  
                            "Assembly {0} not found.", sqlName));  
  
                    return GetAssemblyName(rdr.GetString(0), rdr.GetInt32(1),  
                        rdr.GetInt32(2), rdr.GetInt32(3),  
                        rdr.GetInt32(4), (rdr.IsDBNull(5)  
                        ? SqlString.Null : rdr.GetSqlString(5)),  
                        (rdr.IsDBNull(6) ? SqlBinary.Null : rdr.GetSqlBinary(6)),  
                        rdr.IsDBNull(7) ? SqlString.Null : rdr.GetSqlString(7));  
                }  
                finally  
                {  
                    rdr.Close();  
                }  
            }  
        }  
  
        /// <summary>  
        /// helper function to return the assembly name from   
        /// its components stored in sql metadata  
        /// </summary>  
        /// <param name="friendlyName"></param>  
        /// <param name="major_version"></param>  
        /// <param name="minor_version"></param>  
        /// <param name="build"></param>  
        /// <param name="revision"></param>  
        /// <param name="culture"></param>  
        /// <param name="publicKeyToken"></param>  
        /// <returns></returns>  
        private static string GetAssemblyName(string friendlyName, int majorVersion, int minorVersion,  
            int build, int revision, SqlString culture, SqlBinary publicKeyToken, SqlString processorArchitecture)  
        {  
            StringBuilder sb = new StringBuilder();  
            sb.Append(friendlyName).Append(", ");  
            sb.Append("version=");  
            sb.Append(majorVersion).Append('.');  
            sb.Append(minorVersion).Append('.');  
            sb.Append(build).Append('.');  
            sb.Append(revision).Append(", ");  
            sb.Append("culture=").Append(culture.IsNull ? "neutral" : culture.Value).Append(", ");  
            sb.Append("publickeytoken=");  
            if (publicKeyToken.IsNull)  
            {  
                sb.Append("null");  
            }  
            else  
            {  
                foreach (byte b in publicKeyToken.Value)  
                {  
                    sb.Append(b.ToString("X2", CultureInfo.InvariantCulture));  
                }  
            }  
  
            sb.Append(", ");  
            sb.Append("processorarchitecture=");  
            sb.Append(processorArchitecture.IsNull ? "msil" : processorArchitecture.Value);  
  
            return sb.ToString();  
        }  
  
        private static string ToHexString(byte[] value)  
        {  
            if (value == null)  
                return null;  
  
            StringBuilder sb = new StringBuilder();  
            foreach (byte b in value)  
            {  
                sb.Append(b.ToString("X2", CultureInfo.InvariantCulture));  
            }  
  
            return sb.ToString();  
        }  
  
        #endregion  
    }  
  
```  
  
 <span data-ttu-id="c99e7-137">Visual Basic</span><span class="sxs-lookup"><span data-stu-id="c99e7-137">Visual Basic</span></span>  
  
```  
Imports Microsoft.SqlServer.Server  
Imports Microsoft.VisualBasic  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Diagnostics  
Imports System.Globalization  
Imports System.Reflection  
Imports System.Runtime.InteropServices  
Imports System.Text  
  
''' <summary>  
''' AssemblyBrowser is a simple utility for composing sql queries over   
''' assembly metadata. It uses a table-valued-function to return  
''' a table to SqlServer.  
''' </summary>  
  
Public NotInheritable Class AssemblyBrowser  
    ''' <summary>  
    ''' Get the types in the assembly, as a table  
    ''' </summary>  
    ''' <param name="name"></param>  
    ''' <returns></returns>  
    <Microsoft.SqlServer.Server.SqlFunction(FillRowMethodName:="FillTypeRow", Name:="GetTypes", _  
        TableDefinition:="FullName nvarchar(256), BaseTypeName nvarchar(256), IsValueType bit, NumFields int, IsSerializable bit, IsISerializable bit, IsLayoutSequential bit, Namespace nvarchar(256), IsPublic bit, IsSealed bit, AssemblyName nvarchar(256)")> _  
    Public Shared Function GetTypes(ByVal name As String) As IEnumerable  
        Dim e As IEnumerable  
  
        Try  
            Dim a As [Assembly] = GetAssembly(name)  
            If a Is Nothing Then  
                e = New Type(-1) {}  
            Else  
                e = a.GetTypes()  
            End If  
  
        Catch te As ReflectionTypeLoadException  
            'could not load some of the types, just return the types that you could load  
            e = te.Types  
        End Try  
  
        Return e  
    End Function  
  
    ''' <summary>  
    ''' Called by SQL Server to populate a row in the results of the TVF.  Takes a type and  
    ''' breaks the information up into separate columns for the row being generated.  
    ''' </summary>  
    ''' <param name="row"></param>  
    ''' <param name="fullName"></param>  
    ''' <param name="baseTypeName"></param>  
    ''' <param name="isValueType"></param>  
    ''' <param name="numFields"></param>  
    ''' <param name="isSerializable"></param>  
    ''' <param name="isISerializable"></param>  
    ''' <param name="isLayoutSequential"></param>  
    ''' <param name="namespace"></param>  
    ''' <param name="isPublic"></param>  
    ''' <param name="isSealed"></param>  
    ''' <param name="assemblyName"></param>  
    ''' <remarks></remarks>  
    Public Shared Sub FillTypeRow(ByVal row As Object, <Out()> ByRef fullName As String, <Out()> ByRef baseTypeName As String, _  
        <Out()> ByRef isValueType As Boolean, <Out()> ByRef numFields As Integer, <Out()> ByRef isSerializable As Boolean, _  
        <Out()> ByRef isISerializable As Boolean, <Out()> ByRef isLayoutSequential As Boolean, <Out()> ByRef [namespace] As String, _  
        <Out()> ByRef isPublic As Boolean, <Out()> ByRef isSealed As Boolean, <Out()> ByRef assemblyName As String)  
  
        If row Is Nothing Then  
            Return  
        End If  
  
        Dim t As Type = CType(row, Type)  
  
        fullName = t.FullName  
        If (t.BaseType Is Nothing) Then  
            baseTypeName = String.Empty  
        Else  
            baseTypeName = t.BaseType.FullName  
        End If  
  
        isValueType = t.IsValueType  
  
        Dim fields As FieldInfo() = t.GetFields(BindingFlags.Instance Or BindingFlags.Public)  
  
        If (fields Is Nothing) Then  
            numFields = 0  
        Else  
            numFields = fields.Length  
        End If  
  
        isSerializable = t.IsSerializable  
        isISerializable = GetType(System.Runtime.Serialization.ISerializable).IsAssignableFrom(t)  
        isLayoutSequential = t.IsLayoutSequential  
        [namespace] = t.Namespace  
        isPublic = t.IsPublic  
        isSealed = t.IsSealed  
        assemblyName = t.Assembly.GetName().Name  
    End Sub  
  
    Friend Shared Function GetAssembly(ByVal name As String) As [Assembly]  
        Try  
            Return [Assembly].Load(name)  
        Catch  
            Return Nothing  
        End Try  
    End Function  
  
    Private Sub New()  
    End Sub  
  
    <SqlFunction(FillRowMethodName:="FillAssemblyRow", Name:="GetLoadedAssemblies", _  
        TableDefinition:="FullName nvarchar(256)")> _  
    Public Shared Function GetLoadedAssemblies() As IEnumerable  
        Dim e As IEnumerable = AppDomain.CurrentDomain.GetAssemblies()  
        'Dim schemas() As Microsoft.SqlServer.Server.SqlMetaData = _  
        '    {New Microsoft.SqlServer.Server.SqlMetaData("FullName", _  
        '    SqlDbType.NVarChar, 256)}  
  
        Return e  
    End Function  
    Public Shared Sub FillAssemblyRow(ByVal row As Object, <Out()> ByRef fullName As String)  
        If row Is Nothing Then Throw New ArgumentNullException("row")  
        fullName = CType(row, [Assembly]).FullName  
    End Sub  
End Class  
<Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute(Microsoft.SqlServer.Server.Format.Native), Serializable()> _  
Public Structure SimpleUdt  
    Implements INullable  
#Region "udt contract"  
  
    Public Overrides Function ToString() As String  
        Return Value.ToString()  
    End Function  
  
    Public ReadOnly Property IsNull() As Boolean Implements INullable.IsNull  
        Get  
            Return Me.Value.IsNull  
        End Get  
    End Property  
  
    Public Shared ReadOnly Property Null() As SimpleUdt  
        Get  
            Dim h As New SimpleUdt()  
  
            Return h  
        End Get  
    End Property  
  
    Public Shared Function Parse(ByVal sqlString As SqlString) As SimpleUdt  
        If sqlString.IsNull Then  
            Return Null  
        End If  
  
        Dim simpleUdt As New SimpleUdt()  
  
        simpleUdt.Value = New SqlInt32(Integer.Parse(sqlString.Value, _  
            System.Globalization.CultureInfo.InvariantCulture))  
  
        Return simpleUdt  
    End Function  
#End Region  
  
#Region "implementation"  
    Private privValue As SqlInt32  
  
    Private _examplePublicField As SqlInt32  
  
    Public Property ExamplePublicField() As SqlInt32  
        Get  
            Return Me._examplePublicField  
        End Get  
        Set(ByVal value As SqlInt32)  
            Me._examplePublicField = value  
        End Set  
    End Property  
  
    Public Property Value() As SqlInt32  
        Get  
            Return Me.privValue  
        End Get  
        Set(ByVal value As SqlInt32)  
            Me.privValue = value  
        End Set  
    End Property  
  
    <Microsoft.SqlServer.Server.SqlMethod(IsDeterministic:=True)> _  
    Public Function ReturnValue() As SqlInt32  
        Return Me.privValue  
    End Function  
#End Region  
End Structure  
Public NotInheritable Class UdtServices  
#Region "udt fields"  
  
    ''' <summary>  
    ''' Get the fields in the UDT callable from tsql, as a table  
    ''' </summary>  
    ''' <param name="udtName"></param>  
    ''' <returns></returns>  
    <Microsoft.SqlServer.Server.SqlFunction(FillRowMethodName:="FillFieldRow", Name:="GetFields", TableDefinition:="Name nvarchar(128), Type nvarchar(128), RoutineProperties nvarchar(128)")> _  
    Public Shared Function GetUdtFields(ByVal udtName As String) As IEnumerable  
        Dim fields As ArrayList = GetSqlFields(GetUdt(udtName))  
  
        Return fields  
    End Function  
    Public Shared Sub FillFieldRow(ByVal row As Object, ByRef [name] As String, ByRef type As String)  
        Dim fi As FieldInfo = CType(row, FieldInfo)  
  
        [name] = fi.Name  
        type = fi.FieldType.Name  
    End Sub  
  
#End Region  
  
#Region "udt properties"  
  
    ''' <summary>  
    ''' Get the properties defined in a particular UDT  
    ''' </summary>  
    ''' <param name="udtName"></param>  
    ''' <returns></returns>  
    <Microsoft.SqlServer.Server.SqlFunction(FillRowMethodName:="FillPropertyRow", Name:="GetProperties", TableDefinition:="Name nvarchar(128), Type nvarchar(128), RoutineProperties nvarchar(128)")> _  
    Public Shared Function GetUdtProperties(ByVal udtName As String) As IEnumerable  
        Dim properties As ArrayList = GetSqlProperties(GetUdt(udtName))  
  
        Return properties  
    End Function  
  
    ''' <summary>  
    ''' Called by SQL Server to populate a row of the results of the TVF.    
    ''' </summary>  
    ''' <param name="row"></param>  
    ''' <param name="name"></param>  
    ''' <param name="type"></param>  
    ''' <param name="routineProperties"></param>  
    ''' <remarks></remarks>  
    Public Shared Sub FillPropertyRow(ByVal row As Object, ByRef name As String, ByRef type As String, ByRef routineProperties As String)  
        Dim pi As PropertyInfo = CType(row, PropertyInfo)  
  
        name = pi.Name  
        type = pi.PropertyType.Name  
  
        Dim methInfo As MethodInfo = pi.GetGetMethod()  
        Dim attrs As Object() = methInfo.GetCustomAttributes( _  
            GetType(Microsoft.SqlServer.Server.SqlMethodAttribute), True)  
  
        If Not (attrs Is Nothing) AndAlso attrs.Length = 1 Then  
            Dim attr As Microsoft.SqlServer.Server.SqlMethodAttribute _  
                = CType(attrs(0), Microsoft.SqlServer.Server.SqlMethodAttribute)  
  
            routineProperties = GetRoutineProperties(attr)  
        End If  
    End Sub  
  
#End Region  
  
#Region "udt methods"  
  
    ''' <summary>  
    ''' Get the methods on the UDT callable from tsql, as a table  
    ''' </summary>  
    ''' <param name="udtName"></param>  
    ''' <returns></returns>  
    <Microsoft.SqlServer.Server.SqlFunction(FillRowMethodName:="FillMethodRow", Name:="GetMethods", TableDefinition:="Name nvarchar(128), Parameters nvarchar(4000), Type nvarchar(128), RoutineProperties nvarchar(128)")> _  
    Public Shared Function GetUdtMethods(ByVal udtName As String) As IEnumerable  
        Dim methods As ArrayList = GetSqlMethods(GetUdt(udtName))  
  
        Return methods  
    End Function  
  
    ''' <summary>  
    ''' Called by SQL Server to populate a row being returned by the TVF.  Breaks apart the   
    ''' MethodInfo object into the data which will populate each column of the row being returned.  
    ''' </summary>  
    ''' <param name="row"></param>  
    ''' <param name="name"></param>  
    ''' <param name="parameters"></param>  
    ''' <param name="type"></param>  
    ''' <param name="routineProperties"></param>  
    ''' <remarks></remarks>  
    Public Shared Sub FillMethodRow(ByVal row As Object, ByRef name As String, ByRef parameters As String, _  
        ByRef type As String, ByRef routineProperties As String)  
        Dim methInfo As MethodInfo = CType(row, MethodInfo)  
  
        name = methInfo.Name  
  
        Dim sb As New StringBuilder("(")  
        Dim first As Boolean = True  
  
        Dim pi As ParameterInfo  
        For Each pi In methInfo.GetParameters()  
            If first Then  
                first = False  
            Else  
                sb.Append(", ")  
            End If  
  
            sb.Append(pi.Name).Append(" ").Append(pi.ParameterType.Name)  
        Next pi  
  
        sb.Append(")")  
        parameters = sb.ToString()  
        type = methInfo.ReturnType.Name  
  
        Dim attrs As Object() = methInfo.GetCustomAttributes( _  
            GetType(Microsoft.SqlServer.Server.SqlMethodAttribute), True)  
  
        If Not (attrs Is Nothing) AndAlso attrs.Length = 1 Then  
            Dim attr As Microsoft.SqlServer.Server.SqlMethodAttribute _  
                = CType(attrs(0), Microsoft.SqlServer.Server.SqlMethodAttribute)  
  
            routineProperties = GetRoutineProperties(attr)  
        End If  
    End Sub  
  
#End Region  
  
#Region "internal utility functions"  
    Private Sub New()  
    End Sub  
  
    ''' <summary>  
    ''' Utility function to get the string representation of  
    ''' routine properties on a type  
    ''' </summary>  
    ''' <param name="attr"></param>  
    ''' <returns></returns>  
    Private Shared Function GetRoutineProperties(ByVal attr As Microsoft.SqlServer.Server.SqlMethodAttribute) As String  
        Dim sb As New StringBuilder()  
  
        If attr.OnNullCall Then  
            sb.Append("on_null_call ")  
        End If  
  
        If attr.IsMutator Then  
            sb.Append("mutator ")  
        End If  
  
        If attr.IsDeterministic Then  
            sb.Append("deterministic ")  
        End If  
  
        If attr.IsPrecise Then  
            sb.Append("precise ")  
        End If  
  
        If attr.DataAccess <> Microsoft.SqlServer.Server.DataAccessKind.None Then  
            sb.Append("data_access " & [Enum].GetName( _  
                GetType(Microsoft.SqlServer.Server.DataAccessKind), attr.DataAccess))  
        End If  
  
        Return sb.ToString()  
    End Function  
  
    ''' <summary>  
    ''' Is this a valid parameter type that can be accessible from tsql  
    ''' </summary>  
    ''' <param name="t"></param>  
    ''' <returns></returns>  
    Private Shared Function IsSqlParameterType(ByVal t As Type) As Boolean  
        If validParameterTypes.ContainsKey(t) Then  
            Return True  
        End If  
  
        If t.FullName.StartsWith("System.Data.SqlTypes") Then  
            Return True  
        End If  
  
        If t.GetCustomAttributes( _  
            GetType(Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute), _  
            True).Length = 1 Then  
            Return True  
        End If  
  
        Return False  
    End Function  
  
    ''' <summary>  
    ''' Is the field type valid?  
    ''' </summary>  
    ''' <param name="f"></param>  
    ''' <param name="declaringType"></param>  
    ''' <returns></returns>  
    Private Shared Function IsSqlField(ByVal f As FieldInfo, ByVal declaringType As Type) As Boolean  
        If Not f.DeclaringType Is declaringType Then  
            Return False  
        End If  
  
        Return IsSqlParameterType(f.FieldType)  
    End Function  
  
    ''' <summary>  
    ''' Is the property valid to be called from tsql?  
    ''' </summary>  
    ''' <param name="f"></param>  
    ''' <param name="declaringType"></param>  
    ''' <returns></returns>  
    Private Shared Function IsSqlProperty(ByVal f As PropertyInfo, ByVal declaringType As Type) As Boolean  
        If Not f.DeclaringType Is declaringType Then  
            Return False  
        End If  
  
        Return IsSqlParameterType(f.PropertyType)  
    End Function  
  
    ''' <summary>  
    ''' Is the method valid to be called from tsql?  
    ''' </summary>  
    ''' <param name="m"></param>  
    ''' <param name="declaringType"></param>  
    ''' <returns></returns>  
    Private Shared Function IsSqlMethod(ByVal m As MethodInfo, ByVal declaringType As Type) As Boolean  
        If Not m.DeclaringType Is declaringType Then  
            Return False  
        End If  
  
        Dim info As ParameterInfo  
        For Each info In m.GetParameters()  
            If Not IsSqlParameterType(info.ParameterType) Then  
                Return False  
            End If  
        Next info  
  
        Return IsSqlParameterType(m.ReturnType)  
    End Function  
  
    ''' <summary>  
    ''' Get the udt specified by the clr type name.  
    ''' </summary>  
    ''' <param name="udtName"></param>  
    ''' <returns></returns>  
    Private Shared Function GetUdt(ByVal udtName As String) As Type  
        Return Type.GetType(udtName, True)  
    End Function  
  
    ''' <summary>  
    ''' Get the methods on a type  
    ''' </summary>  
    ''' <param name="t"></param>  
    ''' <returns></returns>  
    Private Shared Function GetSqlMethods(ByVal t As Type) As ArrayList  
        Dim methods As MethodInfo() = t.GetMethods(BindingFlags.Instance Or BindingFlags.Public Or BindingFlags.DeclaredOnly)  
        Dim temp As New ArrayList()  
  
        Dim info As MethodInfo  
        For Each info In methods  
            If IsSqlMethod(info, t) Then  
                temp.Add(info)  
            End If  
        Next info  
  
        Return temp  
    End Function  
  
    ''' <summary>  
    ''' get the properties on a type  
    ''' </summary>  
    ''' <param name="t"></param>  
    ''' <returns></returns>  
    Private Shared Function GetSqlProperties(ByVal t As Type) As ArrayList  
        Dim props As PropertyInfo() = t.GetProperties(BindingFlags.Instance Or BindingFlags.Public Or BindingFlags.DeclaredOnly)  
        Dim temp As New ArrayList()  
  
        Dim info As PropertyInfo  
        For Each info In props  
            If IsSqlProperty(info, t) Then  
                temp.Add(info)  
            End If  
        Next info  
  
        Return temp  
    End Function  
  
    ''' <summary>  
    ''' get the fields on a type  
    ''' </summary>  
    ''' <param name="t"></param>  
    ''' <returns></returns>  
    Private Shared Function GetSqlFields(ByVal t As Type) As ArrayList  
        Dim fields As FieldInfo() = t.GetFields(BindingFlags.Instance Or BindingFlags.Public Or BindingFlags.DeclaredOnly)  
        Dim temp As New ArrayList()  
  
        Dim info As FieldInfo  
        For Each info In fields  
            If IsSqlField(info, t) Then  
                temp.Add(info)  
            End If  
        Next info  
  
        Return temp  
    End Function  
  
    ''' <summary>  
    ''' readonly static used to cache frequently used information  
    ''' </summary>  
    Private Shared ReadOnly validParameterTypes As Hashtable = GetValidParameterTypes()  
  
    ''' <summary>  
    ''' initialize the cached mapping of valid parameter types  
    ''' </summary>  
    Private Shared Function GetValidParameterTypes() As Hashtable  
        Dim validTypes As New Hashtable()  
  
        validTypes(GetType(Boolean)) = True  
        validTypes(GetType(Byte)) = True  
        validTypes(GetType(Short)) = True  
        validTypes(GetType(Char)) = True  
        validTypes(GetType(Integer)) = True  
        validTypes(GetType(Single)) = True  
        validTypes(GetType(Long)) = True  
        validTypes(GetType(Double)) = True  
        validTypes(GetType(String)) = True  
        validTypes(GetType(Guid)) = True  
  
        Return validTypes  
    End Function  
#End Region  
  
#Region "public utility functions"  
  
    <Microsoft.SqlServer.Server.SqlFunction(DataAccess:=Microsoft.SqlServer.Server.DataAccessKind.Read)> _  
    Public Shared Function GetFullAssemblyName(ByVal sqlName As String) As String  
        Using conn As New SqlConnection("context connection=true")  
            Dim cmd As SqlCommand = conn.CreateCommand()  
            cmd.CommandText = "SELECT @sqlName, " _  
                & "assemblyproperty(@sqlName, 'VersionMajor'), " _  
                & "assemblyproperty(@sqlName, 'VersionMinor'), " _  
                & "assemblyproperty(@sqlName, 'VersionBuild'), " _  
                & "assemblyproperty(@sqlName, 'VersionRevision'), " _  
                & "assemblyproperty(@sqlName, 'CultureInfo'), " _  
                & "assemblyproperty(@sqlName, 'PublicKey'), " _  
                & "assemblyproperty(@sqlName, 'Architecture');"  
  
            cmd.Parameters.AddWithValue("@sqlName", sqlName)  
            conn.Open()  
            Dim rdr As SqlDataReader = cmd.ExecuteReader()  
            If Not rdr.Read() Then  
                Throw New ArgumentException( _  
                    String.Format(System.Globalization.CultureInfo.InvariantCulture, _  
                    "Assembly {0} does not exist.", sqlName))  
            End If  
  
            Dim culture As SqlString  
            Dim publicKeyToken As SqlBinary  
  
            If (rdr.IsDBNull(5)) Then  
                culture = SqlString.Null  
            Else  
                culture = rdr.GetSqlString(5)  
            End If  
  
            If (rdr.IsDBNull(6)) Then  
                publicKeyToken = SqlBinary.Null  
            Else  
                publicKeyToken = rdr.GetSqlBinary(6)  
            End If  
  
            Return GetAssemblyName(rdr.GetString(0), rdr.GetInt32(1), rdr.GetInt32(2), _  
                rdr.GetInt32(3), rdr.GetInt32(4), culture, publicKeyToken)  
        End Using  
    End Function  
  
    ''' <summary>  
    ''' Helper function to return the assembly name from   
    ''' its components stored in sql metadata.  
    ''' </summary>  
    ''' <param name="friendlyName"></param>  
    ''' <param name="majorVersion"></param>  
    ''' <param name="minorVersion"></param>  
    ''' <param name="build"></param>  
    ''' <param name="revision"></param>  
    ''' <param name="culture"></param>  
    ''' <param name="publicKeyToken"></param>  
    ''' <returns></returns>  
    Private Shared Function GetAssemblyName(ByVal friendlyName As String, ByVal majorVersion As Integer, ByVal minorVersion As Integer, ByVal build As Integer, ByVal revision As Integer, ByVal culture As SqlString, ByVal publicKeyToken As SqlBinary) As String  
        Dim sb As New StringBuilder()  
        sb.Append(friendlyName).Append(","c)  
        sb.Append("Version=")  
        sb.Append(majorVersion).Append("."c)  
        sb.Append(minorVersion).Append("."c)  
        sb.Append(build).Append("."c)  
        sb.Append(revision).Append(","c)  
        sb.Append("Culture=")  
        If (culture.IsNull) Then  
            sb.Append("neutral")  
        Else  
            sb.Append(culture.Value)  
        End If  
  
        sb.Append(","c)  
        sb.Append("PublicKeyToken=")  
        If publicKeyToken.IsNull Then  
            sb.Append("null")  
        Else  
            Dim b As Byte  
            For Each b In publicKeyToken.Value  
                sb.Append(b.ToString("X2", CultureInfo.InvariantCulture))  
            Next b  
        End If  
  
        Return sb.ToString()  
    End Function  
  
    Private Shared Function ToHexString(ByVal value() As Byte) As String  
        If value Is Nothing Then  
            Return Nothing  
        End If  
  
        Dim sb As New StringBuilder()  
        Dim b As Byte  
  
        For Each b In value  
            sb.Append(b.ToString("X2", CultureInfo.InvariantCulture))  
        Next b  
  
        Return sb.ToString()  
    End Function  
#End Region  
End Class  
```  
  
 <span data-ttu-id="c99e7-138">這是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安裝指令碼 (`Install.sql`)，它會部署組件並在資料庫中建立函數。</span><span class="sxs-lookup"><span data-stu-id="c99e7-138">This is the [!INCLUDE[tsql](../../includes/tsql-md.md)] installation script (`Install.sql`), which deploys the assembly and creates the functions in the database.</span></span>  
  
```  
USE AdventureWorks2012;  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_LoadTest')  
DROP PROCEDURE usp_LoadTest;  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetTypes' AND (type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetTypes];  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetFields' AND (type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetFields];  
GO  
  
IF EXISTS (SELECT * FROM sys.objects where [name] = N'GetProperties' AND (type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetProperties];  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetMethods' AND (type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetMethods];  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetFullAssemblyName' AND (type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetFullAssemblyName];  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetLoadedAssemblies' AND (type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetLoadedAssemblies];  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetClrTypeName' AND (type = 'FN' or type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetClrTypeName];  
GO  
  
IF EXISTS (SELECT * FROM sys.types WHERE [name] = N'SimpleUdt')  
DROP TYPE SimpleUdt;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = N'UDTUtilities')   
DROP ASSEMBLY UDTUtilities;  
GO  
  
USE master  
GO  
  
IF EXISTS (SELECT * FROM sys.server_principals WHERE [name] = 'ExternalSample_Login')  
DROP LOGIN ExternalSample_Login;  
GO  
  
IF EXISTS (SELECT * FROM sys.asymmetric_keys WHERE [name] = 'ExternalSample_Key')  
DROP ASYMMETRIC KEY ExternalSample_Key;  
GO  
  
--Before we register the assembly to SQL Server, we must arrange for the appropriate permissions.  
--Assemblies with unsafe or external_access permissions can only be registered and operate correctly  
--if either the database trustworthy bit is set or if the assembly is signed with a key,  
--that key is registered with SQL Server, a server principal is created from that key,  
--and that principal is granted the external access or unsafe assembly permission.  We choose  
--the latter approach as it is more granular, and therefore safer.  You should never  
--register an assembly with SQL Server (especially with external_access or unsafe permissions) without  
--thoroughly reviewing the source code of the assembly to make sure that its actions   
--do not pose an operational or security risk for your site.  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
set @SamplesPath = 'C:\MySample\'  
EXEC('CREATE ASYMMETRIC KEY ExternalSample_Key FROM EXECUTABLE FILE = ''' + @SamplesPath + 'UDTUtilities.dll'';');  
CREATE LOGIN ExternalSample_Login FROM ASYMMETRIC KEY ExternalSample_Key  
GRANT EXTERNAL ACCESS ASSEMBLY TO ExternalSample_Login  
GO  
  
USE AdventureWorks2012;  
GO  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
set @SamplesPath = 'C:\MySample\'  
  
CREATE ASSEMBLY UDTUtilities FROM @SamplesPath + 'UDTUtilities.dll'  
WITH permission_set=External_Access;  
GO  
  
CREATE FUNCTION [GetTypes](@input nvarchar(4000))   
RETURNS    
TABLE  
(  
    FullName nvarchar(256),  
    BaseTypeName nvarchar(256),  
    IsValueType bit,  
    NumFields int,  
    IsSerializable bit,  
    IsISerializable bit,  
    IsLayoutSequential bit,  
    Namespace nvarchar(256),  
    IsPublic bit,  
    IsSealed bit,  
    AssemblyName nvarchar(256)  
)  
AS EXTERNAL NAME [UDTUtilities].[AssemblyBrowser].[GetTypes];  
GO  
  
CREATE FUNCTION [dbo].[GetLoadedAssemblies]()   
RETURNS   
TABLE  
(  
  FullName nvarchar(256)  
)  
AS EXTERNAL NAME [UDTUtilities].[AssemblyBrowser].[GetLoadedAssemblies]  
GO    
  
CREATE FUNCTION [dbo].[GetFields](@udtName nvarchar(4000))   
RETURNS    
TABLE  
(  
   -- fieldInformation nvarchar(128),  
    Name nvarchar(128),  
    Type nvarchar(128)  
  
)  
AS EXTERNAL NAME [UDTUtilities].[UdtServices].[GetUdtFields];  
GO  
  
CREATE FUNCTION [dbo].[GetProperties](@udtName nvarchar(4000))   
RETURNS    
TABLE  
(  
    Name nvarchar(128),  
    Type nvarchar(128),  
    FieldProperties nvarchar(128)  
)  
AS EXTERNAL NAME [UDTUtilities].[UdtServices].[GetUdtProperties];  
GO  
  
CREATE FUNCTION [dbo].[GetMethods](@udtName nvarchar(4000))   
RETURNS  
TABLE  
(  
    Name nvarchar(128),  
    Parameters nvarchar(4000),  
    Type nvarchar(128),  
    RoutineProperties nvarchar(128)  
)  
AS EXTERNAL NAME [UDTUtilities].[UdtServices].[GetUdtMethods];  
GO  
  
CREATE FUNCTION [dbo].[GetFullAssemblyName](@sqlAsmName nvarchar(128))   
RETURNS nvarchar(4000)  
AS EXTERNAL NAME [UDTUtilities].[UdtServices].[GetFullAssemblyName]  
GO  
  
CREATE FUNCTION [dbo].[GetClrTypeName]  
(  
    @sqlTypeName nvarchar(128)   
)   
RETURNS nvarchar(4000)  
AS  
BEGIN  
    DECLARE @result nvarchar(4000)  
    SELECT @result = st.assembly_class   
    + ','   
      + dbo.GetFullAssemblyName(sa.name)  
    FROM sys.assembly_types st   
        INNER JOIN sys.assemblies sa   
        ON st.assembly_id = sa.assembly_id  
    WHERE st.name = @sqlTypeName;  
  
    RETURN @result;  
END  
GO  
  
CREATE TYPE [dbo].[SimpleUdt]  
EXTERNAL NAME  
[UDTUtilities].[SimpleUdt];  
GO  
  
```  
  
 <span data-ttu-id="c99e7-139">這是 `test.sql`，它會執行函數，藉以測試範例。</span><span class="sxs-lookup"><span data-stu-id="c99e7-139">This is `test.sql`, which tests the sample by executing the functions.</span></span>  
  
```  
  
USE AdventureWorks2012;  
GO  
  
-- Get the full CLR name for UDTUtilities  
SELECT dbo.GetFullAssemblyName(N'UDTUtilities');  
GO  
  
-- Get all the types in this dll  
SELECT * FROM dbo.GetTypes(dbo.GetFullAssemblyName(N'UDTUtilities'));   
GO  
  
-- Get the full CLR name for SimpleUdt  
SELECT dbo.GetClrTypeName('SimpleUdt');  
GO  
  
-- Get the methods on the SimpleUdt type  
SELECT * FROM dbo.GetMethods(dbo.GetClrTypeName('SimpleUdt'));  
GO  
  
-- More complex query to dump all the methods for all the types in the system  
SELECT   
    st.name AS TypeName,   
    methods.Name AS MethodName,   
    methods.Parameters,   
    methods.Type,   
    methods.RoutineProperties   
FROM sys.assembly_types st   
    CROSS APPLY dbo.GetMethods(dbo.GetClrTypeName(st.name)) methods  
GO  
  
```  
  
 <span data-ttu-id="c99e7-140">下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 會從資料庫中移除組件和函數。</span><span class="sxs-lookup"><span data-stu-id="c99e7-140">The following [!INCLUDE[tsql](../../includes/tsql-md.md)] removes the assembly and functions from the database.</span></span>  
  
```  
  
USE AdventureWorks2012;  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_LoadTest')  
DROP PROCEDURE usp_LoadTest;  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetTypes' AND (type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetTypes];  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetFields' AND (type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetFields];  
GO  
  
IF EXISTS (SELECT * FROM sys.objects where [name] = N'GetProperties' AND (type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetProperties];  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetMethods' AND (type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetMethods];  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetFullAssemblyName' AND (type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetFullAssemblyName];  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetLoadedAssemblies' AND (type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetLoadedAssemblies];  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetClrTypeName' AND (type = 'FN' or type = 'FS' OR type = 'FT'))    
DROP FUNCTION [GetClrTypeName];  
GO  
  
IF EXISTS (SELECT * FROM sys.types WHERE [name] = N'SimpleUdt')  
DROP TYPE SimpleUdt;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = N'UDTUtilities')   
DROP ASSEMBLY UDTUtilities;  
GO  
  
USE master;  
GO  
IF EXISTS (SELECT * FROM sys.server_principals WHERE [name] = 'ExternalSample_Login')  
DROP LOGIN ExternalSample_Login;  
GO  
  
IF EXISTS (SELECT * FROM sys.asymmetric_keys WHERE [name] = 'ExternalSample_Key')  
DROP ASYMMETRIC KEY ExternalSample_Key;  
GO  
  
USE AdventureWorks2012;  
GO  
```  
  
## <a name="see-also"></a><span data-ttu-id="c99e7-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c99e7-141">See Also</span></span>  
 [<span data-ttu-id="c99e7-142">通用語言執行平台 &#40;CLR&#41; 整合的使用案例和範例</span><span class="sxs-lookup"><span data-stu-id="c99e7-142">Usage Scenarios and Examples for Common Language Runtime &#40;CLR&#41; Integration</span></span>](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
