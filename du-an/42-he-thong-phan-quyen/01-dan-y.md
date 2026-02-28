Trang-thai: cho-duyet

# Dàn Ý: Hệ Thống Phân Quyền — Hướng Dẫn Toàn Diện (Video Dài)

---

## PHẦN I: MỞ ĐẦU + PHÂN TÍCH VẤN ĐỀ

### Tiêu đề: "Hệ Thống Phân Quyền: Từ Hardcode Đến RBAC/ABAC Chuyên Nghiệp"

---

## 1) Vấn đề ngoại tại (Problem)

**Hiện trạng:**
- Mỗi lần thêm tính năng mới, bạn phải thêm một đống if/else để kiểm tra quyền của user.
- Kiểm tra `if (user.role === 'admin')`, `if (user.id === post.authorId)`, rồi lại thêm điều kiện cho moderator, editor...
- Code phình to, mỗi chỗ check quyền một kiểu, không nhất quán.

**Nguyên nhân:**
- Không biết cách thiết kế hệ thống phân quyền đúng chuẩn (Role-Based Access Control - RBAC hoặc Attribute-Based Access Control - ABAC).
- Hardcode permission ngay trong controller/component vì nghĩ "đơn giản mà".
- Sợ phức tạp hóa vì chưa hiểu được lợi ích của centralized authorization.

**Hệ quả:**
- Code khó bảo trì: Muốn thay đổi quyền của một role, phải sửa ở nhiều chỗ.
- Lỗ hổng bảo mật: Quên check permission ở một endpoint, user có thể truy cập trái phép.
- Khó scale: Thêm role mới = sửa code khắp nơi.

**Cái giá phải trả:**
- **Thời gian:** Lãng phí giờ để debug permission, tìm chỗ nào quên check quyền.
- **Bảo mật:** Rủi ro cao về security breach, dữ liệu nhạy cảm bị truy cập trái phép.
- **Kiến thức:** Không hiểu nguyên lý phân quyền chuẩn, khó xin việc ở các công ty lớn.

---

## 2) Vấn đề nội tại (Agitate)

**Cảm xúc chủ đạo:**
- Bạn thấy mọi người nói về RBAC, ABAC, Permission Matrix... nhưng không biết bắt đầu từ đâu.
- Cảm thấy bất lực khi tính năng phân quyền của mình cứ phình to thành "spaghetti code".

**Nỗi đau thực tế:**
- Mỗi lần có yêu cầu mới ("cho phép editor xem draft của nhau nhưng không được sửa"), bạn lại phải thêm một đống logic rối rắm.
- Sợ refactor vì sợ làm hỏng logic cũ, nhưng cứ để vậy code càng ngày càng tệ.
- Review code bị comment: "Permission check này không đúng chuẩn, nên dùng middleware".

**Niềm tin sai lệch:**
- "Hệ thống phân quyền quá phức tạp, chỉ dành cho các hệ thống lớn"
- "Hardcode if/else cũng được mà, sao phải làm phức tạp"
- "RBAC/ABAC quá khó, mình không cần thiết phải học"

**Đồng cảm:**
- Điều này rất phổ biến ở developer mới hoặc làm pet project. Vấn đề không phải bạn không giỏi, mà là **chưa được hướng dẫn cách thiết kế hệ thống phân quyền đúng đắn**.

---

## 3) Giải pháp (Solution)

**Hướng dẫn từng bước xây dựng hệ thống phân quyền:**

### A) Hiểu Khái Niệm Cốt Lõi

**1. Authentication vs Authorization**
- **Authentication:** Xác thực "Bạn là ai?" (Login, JWT, Session)
- **Authorization:** Phân quyền "Bạn được làm gì?" (Permission check)

**2. Các mô hình phân quyền:**
- **ACL (Access Control List):** Permission gắn trực tiếp với user
- **RBAC (Role-Based Access Control):** User có Role, Role có Permission
- **ABAC (Attribute-Based Access Control):** Dựa vào attributes (user, resource, context)

### B) RBAC - Mô Hình Phổ Biến Nhất

**Cấu trúc:**
```
User → Role → Permission
```

**Ví dụ:**
- **User:** John Doe
- **Role:** Editor
- **Permission:** `posts:read`, `posts:create`, `posts:update:own`

**Thiết kế Database:**
```sql
users (id, name, email, password)
roles (id, name, description)
permissions (id, name, resource, action)
user_roles (user_id, role_id)
role_permissions (role_id, permission_id)
```

**Middleware kiểm tra quyền:**
```javascript
function authorize(permission) {
  return (req, res, next) => {
    const user = req.user;
    if (!user.hasPermission(permission)) {
      return res.status(403).json({ error: 'Forbidden' });
    }
    next();
  };
}

// Sử dụng
app.delete('/posts/:id', authorize('posts:delete'), deletePost);
```

### C) ABAC - Phân Quyền Linh Hoạt Hơn

**Cấu trúc:**
```
Decision = Policy(User Attributes, Resource Attributes, Context)
```

**Ví dụ:**
- Cho phép sửa bài viết nếu:
  - User là author của bài
  - HOẶC User là admin
  - VÀ Bài viết chưa bị lock

**Policy Engine:**
```javascript
const policy = {
  'posts:update': (user, post, context) => {
    if (user.role === 'admin') return true;
    if (post.authorId === user.id && !post.locked) return true;
    return false;
  }
};

function checkPolicy(action, user, resource, context) {
  return policy[action](user, resource, context);
}
```

---

## PHẦN II: HƯỚNG DẪN THỰC HÀNH

### 1) Thiết Kế Database Schema

**Bảng Users, Roles, Permissions**

**users:**
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  name VARCHAR(255),
  created_at TIMESTAMP DEFAULT NOW()
);
```

**roles:**
```sql
CREATE TABLE roles (
  id UUID PRIMARY KEY,
  name VARCHAR(50) UNIQUE NOT NULL,
  description TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);
```

**permissions:**
```sql
CREATE TABLE permissions (
  id UUID PRIMARY KEY,
  name VARCHAR(100) UNIQUE NOT NULL,
  resource VARCHAR(50),
  action VARCHAR(50),
  description TEXT
);
```

**user_roles (Many-to-Many):**
```sql
CREATE TABLE user_roles (
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  role_id UUID REFERENCES roles(id) ON DELETE CASCADE,
  PRIMARY KEY (user_id, role_id)
);
```

**role_permissions (Many-to-Many):**
```sql
CREATE TABLE role_permissions (
  role_id UUID REFERENCES roles(id) ON DELETE CASCADE,
  permission_id UUID REFERENCES permissions(id) ON DELETE CASCADE,
  PRIMARY KEY (role_id, permission_id)
);
```

### 2) Seed Data Mẫu

**Roles:**
```javascript
const roles = [
  { name: 'admin', description: 'Full system access' },
  { name: 'editor', description: 'Can create and edit content' },
  { name: 'viewer', description: 'Read-only access' }
];
```

**Permissions:**
```javascript
const permissions = [
  { name: 'posts:create', resource: 'posts', action: 'create' },
  { name: 'posts:read', resource: 'posts', action: 'read' },
  { name: 'posts:update', resource: 'posts', action: 'update' },
  { name: 'posts:delete', resource: 'posts', action: 'delete' },
  { name: 'users:manage', resource: 'users', action: 'manage' }
];
```

**Gán permission cho role:**
```javascript
// Admin: All permissions
// Editor: posts:create, posts:read, posts:update
// Viewer: posts:read
```

### 3) Backend Implementation (Node.js/Express)

**Model: User với methods kiểm tra quyền:**
```javascript
class User {
  async getRoles() {
    return await db.query(`
      SELECT r.* FROM roles r
      JOIN user_roles ur ON r.id = ur.role_id
      WHERE ur.user_id = $1
    `, [this.id]);
  }
  
  async getPermissions() {
    return await db.query(`
      SELECT DISTINCT p.* FROM permissions p
      JOIN role_permissions rp ON p.id = rp.permission_id
      JOIN user_roles ur ON rp.role_id = ur.role_id
      WHERE ur.user_id = $1
    `, [this.id]);
  }
  
  async hasPermission(permissionName) {
    const permissions = await this.getPermissions();
    return permissions.some(p => p.name === permissionName);
  }
  
  async hasRole(roleName) {
    const roles = await this.getRoles();
    return roles.some(r => r.name === roleName);
  }
}
```

**Middleware Authorize:**
```javascript
function authorize(permission) {
  return async (req, res, next) => {
    try {
      const user = req.user; // Từ authentication middleware
      
      if (!user) {
        return res.status(401).json({ error: 'Unauthorized' });
      }
      
      const hasPermission = await user.hasPermission(permission);
      
      if (!hasPermission) {
        return res.status(403).json({ 
          error: 'Forbidden',
          message: `You need '${permission}' permission`
        });
      }
      
      next();
    } catch (error) {
      return res.status(500).json({ error: 'Server error' });
    }
  };
}
```

**Routes với Authorization:**
```javascript
// Posts routes
router.get('/posts', authorize('posts:read'), getPosts);
router.post('/posts', authorize('posts:create'), createPost);
router.put('/posts/:id', authorize('posts:update'), updatePost);
router.delete('/posts/:id', authorize('posts:delete'), deletePost);

// Admin routes
router.get('/admin/users', authorize('users:manage'), getUsers);
```

### 4) Frontend Integration (React)

**Context cho permissions:**
```jsx
const PermissionContext = createContext();

function PermissionProvider({ children }) {
  const [permissions, setPermissions] = useState([]);
  
  useEffect(() => {
    // Fetch user permissions
    fetchCurrentUserPermissions().then(setPermissions);
  }, []);
  
  const hasPermission = (permission) => {
    return permissions.includes(permission);
  };
  
  return (
    <PermissionContext.Provider value={{ permissions, hasPermission }}>
      {children}
    </PermissionContext.Provider>
  );
}
```

**Component có điều kiện:**
```jsx
function PostActions({ post }) {
  const { hasPermission } = useContext(PermissionContext);
  
  return (
    <div>
      {hasPermission('posts:update') && (
        <button onClick={() => editPost(post.id)}>Edit</button>
      )}
      {hasPermission('posts:delete') && (
        <button onClick={() => deletePost(post.id)}>Delete</button>
      )}
    </div>
  );
}
```

**Higher-Order Component:**
```jsx
function withPermission(Component, permission) {
  return function PermissionGuard(props) {
    const { hasPermission } = useContext(PermissionContext);
    
    if (!hasPermission(permission)) {
      return <div>Access Denied</div>;
    }
    
    return <Component {...props} />;
  };
}

// Sử dụng
const ProtectedAdminPanel = withPermission(AdminPanel, 'users:manage');
```

---

## PHẦN III: NÂNG CAO

### 1) Resource-Based Permissions (Ownership)

**Ví dụ:** Editor chỉ sửa được bài của mình.

**Policy:**
```javascript
async function canUpdatePost(user, postId) {
  // Admin được phép
  if (await user.hasRole('admin')) return true;
  
  // Editor chỉ sửa bài của mình
  if (await user.hasPermission('posts:update')) {
    const post = await Post.findById(postId);
    return post.authorId === user.id;
  }
  
  return false;
}
```

**Middleware:**
```javascript
function authorizeResource(permission, resourceLoader) {
  return async (req, res, next) => {
    const user = req.user;
    const resource = await resourceLoader(req);
    
    const allowed = await canAccessResource(user, permission, resource);
    
    if (!allowed) {
      return res.status(403).json({ error: 'Forbidden' });
    }
    
    req.resource = resource;
    next();
  };
}

// Sử dụng
router.put('/posts/:id', 
  authorizeResource('posts:update', (req) => Post.findById(req.params.id)),
  updatePost
);
```

### 2) Dynamic Permissions (Context-Based)

**Ví dụ:** Chỉ được approve post trong giờ làm việc.

**Policy Engine:**
```javascript
const policies = {
  'posts:approve': (user, post, context) => {
    if (!user.hasPermission('posts:approve')) return false;
    
    // Chỉ trong giờ làm việc
    const hour = new Date().getHours();
    if (hour < 9 || hour > 17) return false;
    
    // Không approve bài của chính mình
    if (post.authorId === user.id) return false;
    
    return true;
  }
};
```

### 3) Hierarchical Roles

**Ví dụ:** Super Admin > Admin > Moderator > User

**Implementation:**
```javascript
const roleHierarchy = {
  'super_admin': ['admin', 'moderator', 'user'],
  'admin': ['moderator', 'user'],
  'moderator': ['user'],
  'user': []
};

async function hasRoleOrHigher(user, requiredRole) {
  const userRoles = await user.getRoles();
  
  for (const role of userRoles) {
    if (role.name === requiredRole) return true;
    if (roleHierarchy[role.name]?.includes(requiredRole)) return true;
  }
  
  return false;
}
```

### 4) Caching Permissions

**Tránh query DB mỗi request:**

```javascript
const redis = require('redis');
const client = redis.createClient();

async function getUserPermissions(userId) {
  // Check cache
  const cached = await client.get(`permissions:${userId}`);
  if (cached) return JSON.parse(cached);
  
  // Query DB
  const permissions = await db.query(`
    SELECT DISTINCT p.name FROM permissions p
    JOIN role_permissions rp ON p.id = rp.permission_id
    JOIN user_roles ur ON rp.role_id = ur.role_id
    WHERE ur.user_id = $1
  `, [userId]);
  
  // Cache 1 hour
  await client.setex(`permissions:${userId}`, 3600, JSON.stringify(permissions));
  
  return permissions;
}
```

---

## PHẦN IV: BEST PRACTICES

### 1) Nguyên Tắc Thiết Kế

**a) Principle of Least Privilege:**
- Chỉ cấp quyền tối thiểu cần thiết
- Không set default là admin

**b) Separation of Concerns:**
- Authentication ≠ Authorization
- Tách riêng logic kiểm tra quyền ra middleware/service

**c) Deny by Default:**
- Mặc định là từ chối
- Chỉ cho phép khi có rule rõ ràng

### 2) Security Considerations

**a) Validate mọi input:**
```javascript
// Không tin frontend
if (!hasPermission('posts:delete')) {
  // Backend phải check lại
}
```

**b) Log mọi quyết định authorize:**
```javascript
logger.info({
  action: 'authorization',
  user: user.id,
  permission,
  resource,
  decision: allowed
});
```

**c) Audit trail:**
```sql
CREATE TABLE audit_logs (
  id UUID PRIMARY KEY,
  user_id UUID,
  action VARCHAR(100),
  resource_type VARCHAR(50),
  resource_id UUID,
  decision BOOLEAN,
  timestamp TIMESTAMP DEFAULT NOW()
);
```

### 3) Testing

**Unit test policies:**
```javascript
describe('Permission Policy', () => {
  it('admin can delete any post', async () => {
    const admin = createUser({ role: 'admin' });
    const post = createPost({ authorId: 'other-user' });
    
    const result = await canDeletePost(admin, post);
    expect(result).toBe(true);
  });
  
  it('editor cannot delete others post', async () => {
    const editor = createUser({ role: 'editor' });
    const post = createPost({ authorId: 'other-user' });
    
    const result = await canDeletePost(editor, post);
    expect(result).toBe(false);
  });
});
```

---

## PHẦN V: CÔNG CỤ VÀ THƯ VIỆN

### 1) Backend Libraries

**Node.js:**
- `accesscontrol` - RBAC implementation
- `casbin` - Policy authorization library (support ABAC)
- `permit.io` - Cloud authorization service

**Python:**
- `django-guardian` - Object-level permissions
- `flask-principal` - Identity & permission management
- `casbin` - Policy engine

### 2) Cloud Services

**Auth0:**
- Built-in RBAC
- API authorization

**AWS IAM:**
- Policy-based access control
- Fine-grained permissions

**Permit.io:**
- Authorization as a service
- UI for managing roles/permissions

### 3) Standards & Frameworks

**XACML** (eXtensible Access Control Markup Language)
**OAuth 2.0 Scopes** - API permissions
**OpenID Connect** - Identity layer

---

## PHẦN VI: KẾT LUẬN

### Tóm Tắt Hành Trình

**Từ:**
- Hardcode if/else permission khắp nơi
- Code rối, khó maintain, dễ lỗ hổng

**Đến:**
- Hệ thống phân quyền rõ ràng (RBAC/ABAC)
- Centralized authorization
- Dễ mở rộng, bảo mật tốt

### Next Steps

**1. Học thêm:**
- OAuth 2.0 & OpenID Connect
- Zero Trust Architecture
- Policy as Code

**2. Thực hành:**
- Xây dựng hệ thống phân quyền cho project
- Implement RBAC cho API
- Tích hợp ABAC cho business rules

**3. Nâng cao:**
- Multi-tenancy permissions
- Microservices authorization
- Distributed authorization

---

## CTA: Khóa Học 1-Kèm-1 LetDiv

"Nếu bạn muốn được hướng dẫn chi tiết, review code, và xây dựng hệ thống phân quyền production-ready, tham gia khóa học 1 kèm 1 tại LetDiv. Mentor sẽ hỗ trợ bạn từng bước, đảm bảo bạn nắm vững từ lý thuyết đến thực chiến."

**Link đăng ký:** [LetDiv Course Registration]

---
