# NIT3122 --- Enterprise Network Management

# Mock Final Examination（模拟期末试卷）

> **总分：100 分｜建议时间：90--120 分钟**
>
> 命题依据：2022/2021 Sample Final Exam、课程 Learning
> Outcomes、九个课程模块及实验相关考点。
>
> **重要说明：**
> 本卷是基于现有材料设计的高相关性模拟题，不是正式考试预测。题目采用样卷的英文表达风格，覆盖原卷高频主题，并加入原样卷未充分考查的课程知识点。

------------------------------------------------------------------------

# Part A --- Question Paper

## Question 1 --- Password Policy（10 Marks）

A company is reviewing its password policy. The IT department proposes
increasing the minimum password length and requiring users to change
their passwords more frequently.

**Analyse the advantages and disadvantages of implementing a very strict
password policy. Explain how an organization can maintain a balance
between security and usability.**

------------------------------------------------------------------------

## Question 2 --- Group Policy Processing（10 Marks）

An administrator has configured different Group Policy Objects (GPOs) at
the Local, Site, Domain and Organizational Unit (OU) levels.

1.  Explain the order in which these policies are processed.
2.  Give an example to illustrate what happens when two GPOs configure
    conflicting settings.
3.  Explain the purpose of **Enforced** and **Block Inheritance**.

------------------------------------------------------------------------

## Question 3 --- Fine-Grained Password Policy（10 Marks）

A company wants its IT administrators to use a stronger password policy
than ordinary employees. All administrator accounts are placed in an OU
named `IT_Admin`.

**Describe the steps required to configure a separate password policy
for these administrators. Explain why the policy cannot simply be linked
to the `IT_Admin` OU.**

------------------------------------------------------------------------

## Question 4 --- RODC and Password Replication Policy（10 Marks）

A company plans to deploy a Read-Only Domain Controller (RODC) at a
small branch office. The branch office does not have a secure server
room.

1.  Explain the differences between a writable Domain Controller (DC)
    and an RODC.
2.  Explain why an RODC is suitable for this branch office.
3.  What is the purpose of Password Replication Policy (PRP)?
4.  A user's password has not been cached on the RODC. Explain whether
    the user can sign in when the RODC can and cannot contact a writable
    DC.

------------------------------------------------------------------------

## Question 5 --- DNS Aging and Scavenging（10 Marks）

A company has many computers that frequently change IP addresses. Its
DNS zone contains resource records for computers that have already been
removed from the network.

1.  Explain what **DNS Aging** and **Scavenging** are.
2.  Describe the basic configuration required to enable these functions.
3.  Analyse two problems that may occur if Aging and Scavenging are not
    configured.

------------------------------------------------------------------------

## Question 6 --- Group Policy Filtering（10 Marks）

An administrator wants a GPO to apply only to computers running Windows
Server 2016. Other computers in the same Organizational Unit should not
receive this policy.

1.  Explain how **WMI Filtering** can be used to meet this requirement.
2.  Explain the difference between WMI Filtering and Security Filtering.
3.  Give one example of a situation where an administrator may use each
    filtering method.

------------------------------------------------------------------------

## Question 7 --- Active Directory Trust Relationships（10 Marks）

Two companies, Alpha Ltd and Beta Ltd, have separate Active Directory
forests. After a merger, employees from both companies need to access
selected resources in the other company's forest.

1.  Recommend a suitable trust relationship.
2.  Explain the difference between a one-way trust and a two-way trust.
3.  Explain what is meant by a transitive trust.
4.  Does establishing a trust automatically grant users permission to
    access all resources? Explain your answer.

------------------------------------------------------------------------

## Question 8 --- PKI and Active Directory Certificate Services（10 Marks）

An organization wants to use digital certificates to secure internal
services and verify the identity of users and computers.

1.  Explain the role of a Certificate Authority (CA).
2.  Describe how Active Directory Certificate Services (AD CS) supports
    an organization's Public Key Infrastructure (PKI).
3.  Explain the purpose of a Certificate Revocation List (CRL).
4.  Give one example of how digital certificates can be used in an
    enterprise network.

------------------------------------------------------------------------

## Question 9 --- Enterprise Network Design（20 Marks）

GlobalTech is a company using Windows Server 2016 and Active Directory.
Its headquarters is located in Singapore. It has three departments:

-   Finance, located at the Singapore headquarters.
-   Production, located in Kuala Lumpur.
-   Sales, located in Bangkok.

The company recently acquired another company, DataWorks, which
currently operates its own Active Directory forest.

Answer the following questions:

1.  Propose an appropriate Active Directory forest and domain structure
    for GlobalTech. Draw a diagram and label the domain names and
    physical locations. (6 Marks)
2.  Explain the differences between a Forest, Domain, Domain Tree and
    Organizational Unit (OU). (6 Marks)
3.  Explain how AD Sites can be used to represent the different physical
    locations. (3 Marks)
4.  Recommend a trust relationship between GlobalTech and DataWorks if
    both companies retain their own forests. Explain your choice. (5
    Marks)

------------------------------------------------------------------------

# Part B --- Suggested Answers

> 以下答案是参考作答框架。考试时不要求逐字背诵，但应写出关键术语、原因和场景。

## Q1 --- Suggested Answer

A strict password policy can improve security by requiring longer and
more complex passwords. It can make passwords harder to guess.

However, excessive restrictions and frequent password changes may cause
users to forget their passwords. This increases password reset requests,
service desk workload and organizational costs. Users may also write
passwords down or reuse predictable passwords.

An organization should balance security and usability by setting
reasonable password requirements and avoiding unnecessary password
changes.

**中文理解：**
过严提高密码强度，但可能增加遗忘、重置和管理成本；过松则容易被猜测。核心是安全与可用性之间的平衡。

------------------------------------------------------------------------

## Q2 --- Suggested Answer

GPOs are normally processed in the **LSDOU** order:

1.  Local
2.  Site
3.  Domain
4.  Organizational Unit (OU)

When conflicting settings exist, a later-applied policy normally
overrides an earlier policy.

For example, a Site GPO sets a blue desktop wallpaper, while an OU GPO
sets a green wallpaper. Normally, the OU setting takes effect.

**Enforced** prevents lower-level GPOs from overriding the enforced
settings. It can also override Block Inheritance.

**Block Inheritance** prevents normal GPO inheritance from higher
levels, but it does not block an enforced GPO.

**中文理解：** 先记
LSDOU。普通情况下后应用的冲突设置覆盖先应用的设置；Enforced
可以保护上级策略，Block Inheritance 则阻止普通上级策略向下继承。

------------------------------------------------------------------------

## Q3 --- Suggested Answer

1.  Create a Global Security Group named `IT_Administrators`.
2.  Add all administrator user accounts from the `IT_Admin` OU to this
    group.
3.  Create a Password Settings Object (PSO).
4.  Configure the required password settings in the PSO.
5.  Apply the PSO to the `IT_Administrators` security group.

Fine-Grained Password Policies (FGPP) can be applied to individual user
accounts or global security groups, but cannot be directly linked to an
OU.

**中文理解：** FGPP 不能直接作用于
OU。需要创建全局安全组，把管理员放进去，再把 PSO 应用到安全组。

------------------------------------------------------------------------

## Q4 --- Suggested Answer

A writable DC stores and manages Active Directory data and allows
directory changes. An RODC stores a read-only copy of Active Directory
and caches passwords only for selected users.

An RODC is suitable for a branch office with poor physical security
because it reduces the risk of exposing all domain credentials if the
server is stolen.

**Password Replication Policy (PRP)** determines which users' passwords
are allowed or denied to be cached on the RODC.

If a user's password has not been cached:

-   If the RODC can contact a writable DC, it can forward the
    authentication request to that DC.
-   If the RODC cannot contact a writable DC, the user normally cannot
    sign in because the required credentials are not available locally.

**中文理解：** RODC 适合缺少安全机房的分支机构。PRP
控制哪些密码可以缓存。未缓存的用户需要联系可写 DC
完成认证；如果联系不上，就无法登录。

------------------------------------------------------------------------

## Q5 --- Suggested Answer

**Aging** determines whether DNS resource records have become stale
based on their timestamps and configured time periods.

**Scavenging** removes stale DNS resource records that meet the
configured conditions.

Basic configuration:

1.  Enable timestamps for dynamically added DNS resource records.
2.  Configure the aging time periods, including the relevant refresh
    settings.
3.  Enable scavenging to remove stale records.

Problems if not configured:

-   DNS queries may return outdated records and incorrect IP addresses.
-   Stale records may accumulate, increasing the size of DNS zones and
    affecting server performance.
-   A DNS name may point to an IP address that has been reassigned to
    another device.

**中文理解：** Aging 判断记录是否陈旧，Scavenging
删除符合条件的陈旧记录。不配置会造成错误解析、记录堆积和性能问题。

------------------------------------------------------------------------

## Q6 --- Suggested Answer

**WMI Filtering** uses Windows Management Instrumentation queries to
identify computers that meet specified system conditions.

For example, an administrator can create a WMI filter that checks the
operating system version and link it to a GPO. The policy will apply
only to computers that satisfy the filter.

**Security Filtering** determines which users or computers have
permission to apply a GPO.

Examples:

-   WMI Filtering: Apply a policy only to computers running Windows
    Server 2016.
-   Security Filtering: Apply a policy only to members of the
    `IT_Admins` security group.

**中文理解：** WMI Filtering
根据计算机属性筛选，例如操作系统版本；Security Filtering
根据用户或计算机的安全组权限决定是否应用 GPO。

------------------------------------------------------------------------

## Q7 --- Suggested Answer

A **Forest Trust** is suitable when Alpha Ltd and Beta Ltd retain
separate Active Directory forests but need to access resources across
the forests.

-   **One-way trust:** One forest trusts the other forest for
    authentication in one direction.
-   **Two-way trust:** Each forest trusts the other forest.
-   **Transitive trust:** Trust can extend beyond the directly connected
    domains or forests, according to the trust configuration.

Establishing a trust does not automatically grant access to all
resources. Administrators must still assign appropriate permissions to
users and groups.

**中文理解：** 两家公司各自保留独立 Forest，通常考虑 Forest
Trust。单向和双向描述信任方向；可传递描述信任能否延伸。建立信任不等于自动获得资源权限。

------------------------------------------------------------------------

## Q8 --- Suggested Answer

A **Certificate Authority (CA)** is responsible for issuing and managing
digital certificates.

**Active Directory Certificate Services (AD CS)** provides an enterprise
PKI solution. It allows an organization to issue, manage and validate
certificates for users, computers and services.

A **Certificate Revocation List (CRL)** contains certificates that have
been revoked before their expiration date. Systems can check the CRL to
determine whether a certificate should still be trusted.

Examples of certificate usage include:

-   Securing web services with HTTPS.
-   Authenticating users or computers.
-   Supporting encryption such as IPsec or EFS.

**中文理解：** CA 负责颁发证书；AD CS 为企业提供证书管理体系；CRL
用于检查证书是否已被提前吊销。证书可以用于 HTTPS、身份认证和加密。

------------------------------------------------------------------------

## Q9 --- Suggested Answer

### 1. Proposed Forest and Domain Structure

One possible design is to use one forest and one domain for GlobalTech:

``` text
Forest: globaltech.com
└── Domain: globaltech.com
    ├── OU: Finance (Singapore)
    ├── OU: Production (Kuala Lumpur)
    └── OU: Sales (Bangkok)

Separate Forest:
dataworks.com
└── Domain: dataworks.com
```

Departments can be organized using OUs. Separate physical locations can
be represented using AD Sites.

### 2. Key Concepts

-   **Forest:** The highest-level Active Directory structure, which can
    contain one or more domains.
-   **Domain:** An administrative and security boundary within Active
    Directory.
-   **Domain Tree:** A group of domains that share a contiguous DNS
    namespace.
-   **OU:** A container used to organize users, groups and computers,
    and to apply or delegate administration.

### 3. AD Sites

Create separate AD Sites for Singapore, Kuala Lumpur and Bangkok, and
associate the appropriate IP subnets with each site. This helps Active
Directory understand the physical network topology and manage
replication between locations.

### 4. Trust Relationship

If GlobalTech and DataWorks retain separate forests, establish a Forest
Trust. A two-way trust may be used if both organizations require
authentication across the forests.

Resource permissions must still be configured separately.

**中文理解：** GlobalTech 可以采用一个 Forest、一个 Domain，三个部门用
OU 组织，三个城市用 AD Sites 表示。DataWorks 保留独立森林时，可通过
Forest Trust 建立跨森林信任。信任关系与资源授权是两回事。

------------------------------------------------------------------------

# Part C --- Last-Minute Coverage Checklist

以下是本模拟卷涉及的关键知识点，以及原样卷没有充分展开但值得快速检查的内容。

  -----------------------------------------------------------------------
  Topic                               Must-know terms
  ----------------------------------- -----------------------------------
  Password Policy                     Complexity, Length, Expiration,
                                      Account Lockout, Usability

  Group Policy                        LSDOU, Enforced, Block Inheritance

  FGPP                                PSO, Global Security Group, User
                                      Account

  RODC                                Read-only, PRP, Password Cache,
                                      Writable DC

  DNS                                 Aging, Scavenging, Timestamp, Stale
                                      Records

  GPO Filtering                       WMI Filtering, Security Filtering

  Trust                               One-way, Two-way, Transitive,
                                      Forest Trust

  PKI                                 CA, AD CS, Certificate, CRL

  Architecture                        Forest, Domain, Domain Tree, OU, AD
                                      Sites
  -----------------------------------------------------------------------

## 如果剩余时间很少，优先掌握

1.  **GPO：** LSDOU、Enforced、Block Inheritance、WMI Filtering。
2.  **密码策略：** FGPP、PSO、Security Group。
3.  **RODC：** PRP、密码缓存、断网登录判断。
4.  **Trust：** Forest Trust、单向/双向、可传递性。
5.  **AD 架构：** Forest、Domain、OU、AD Sites。
6.  **DNS 与 DFS：** Aging/Scavenging、DFS-N/DFS-R。
7.  **PKI：** CA、AD CS、CRL。
8.  **实验题：** 对象类型选择、IIS 与 RMS 的职责。

> **作答提醒：** 分析题不要只写名词。尽量使用"定义 → 原因 → 场景/例子 →
> 结果"的顺序，每个关键点写成完整英文句子。
