# Request Lifecycle 
là quá trình mà một yêu cầu HTTP đi qua từ khi nó được gửi đến ứng dụng Laravel cho đến khi nó nhận lại được phản hồi. Đây là một quá trình quan trọng vì nó quản lý cách mà Laravel xử lý một yêu cầu, bao gồm cả việc khởi tạo ứng dụng, xử lý yêu cầu, và trả về kết quả cho người dùng. 
## Khởi tạo
### public/index.php :
Đây là điểm vào chính của tẩt cả các yêu cầu tron trong một ứng dụng Laravel. Tất cả các yêu cầu HTTP sẽ đi qua tệp này đầu tiên.
### Autuloader :
Laravel sử dụng Composer để tự động nạp các tệp cần thiết: Composer sẽ nạp các tệp và thư viện được yêu cầu trong ứng dụng
### Bootstrapping: 
Laravel sẽ tải các tệp cấu hình và các service provider. Service provider là nơi khởi tạo các dịch vụ cần thiết cho ứng dụng.
## HTTP Kernel
### HTTP Kernel :
Tất cả các yêu cầu HTTP đều được xử lý bởi lớp "App\Http\Kernel" . Kernel sẽ định nghĩa một loại các middleware mà yêu cầu cần phải đi qua.
### Middleware :
là các lớp được sử dụng để lọc các yêu cầu HTTP. Các Middleware nhưu kiểm tra xác thực, xử lý session, CSRF, v.v. sẽ được áp dụng tại đây.
## Routing
### Route Service Provider :
Laravel sẽ sử dụng Route Service Provider để đăng ký tất cả các tuyến (Routes) trong ứng dụng. Yêu cầu sẽ được chuyển đến route phù hợp dựa trên URL và phương thức HTTP.
### Route Middleware :
Trước khi xử lý yêu cầu, Laravel có thể áp dụng các Middleware cụ thể cho từng route.
## Controller / Action
### Controller :
Nếu một route được gắn với một controller, yêu cầu sẽ được chuyển đến controller và phương thức thích hợp. Controller sẽ được chứa logic để xử lý yêu cầu, tương tác với cơ sở dữ liệu, và chuẩn bị phản hồi.
### Closures / Callbacks :
Trong trường hợp route được gắn với closure hoặc callback, nó sẽ được thực hiện tại đây.
## View Rendering
Nếu controller hoặc route xử lý yêu cầu trả về một view, Laravel sẽ sử dụng hệ thống view để tạo HTML từ các tệp Blade
## Sending Response
Sau khi controller hoàn thành xử lý yêu cầu, một đối tượng "Response" sẽ được trả về và gửi lại cho người dùng
## Terminate Middleware
Sau khi gửi phản hồi được gửi đi, Laravel sẽ chạy các middleware có phương thức "terminate" để thực hiện các hành động sau khi phản hồi đã được gửi


# Service Container
 là một công cụ quản lý sự phụ thuộc (dependency injection container) mạnh mẽ, được sử dụng để quản lý các class, interface, và các phụ thuộc của chúng. Nó giúp giải quyết các vấn đề về quản lý sự phụ thuộc của các thành phần trong ứng dụng một cách dễ dàng và hiệu quả.
## Các khái niệm chính
### Dependency Injection :
là một thiết kế giúp một class nhận các đối tượng mà nó phụ thuộc vào (dependencies) từ bên ngoài thay vì tự tạo ra chúng. Laravel Service Container tự động tiêm các phụ thuộc vào class khi chúng được khởi tạo.
### Binding :
Quá trình đăng ký (binding) một lớp hoặc một interface vào Service Container. Khi một lớp hoặc interface được "bind" vào Service Container, Laravel sẽ biết cách khởi tạo đối tượng của lớp đó khi cần thiết.
### Resolving :
Khi bạn yêu cầu một đối tượng từ Service Container, quá trình tạo ra đối tượng này được gọi là "resolving". Service Container sẽ tự động tiêm tất cả các phụ thuộc cần thiết vào đối tượng.
## Cách sử dụng 
### Binding
Bạn có thể bind một lớp hoặc một interface vào Service Container bằng cách sử dụng phương thức "bind" hoặc "singleton" trong một Service Provider hoặc trong bootstrap file.
### Resolving :
Sau khi bạn đã bind một lớp hoặc interface vào Service Container, bạn có thể resolve nó ở bất cứ đâu trong ứng dụng.
### Automatic Resolution
Laravel Service Container cũng có khả năng tự động resolve các class mà không cần phải bind trước, miễn là các class này có thể được khởi tạo một cách rõ ràng (nghĩa là có thể tự động tiêm tất cả các phụ thuộc).


# Service Providers
là trung tâm của toàn bộ quá trình khởi tạo ứng dụng. Chúng chịu trách nhiệm bind các dịch vụ vào Service Container và chuẩn bị mọi thứ mà ứng dụng cần để hoạt động, như kết nối cơ sở dữ liệu, đăng ký các route, đăng ký các event listener, hoặc bind các dịch vụ của bên thứ ba vào Service Container.
## Các chức năng chính
### Binding :
thường dùng để bind các dịch vụ, class, hoặc các đối tượng vào Service Container. Điều này cho phép các thành phần khác của ứng dụng có thể dễ dàng sử dụng các dịch vụ này.
### Bootstrapping :
cung cấp phương thức "boot" để thực hiện các hành động cần thiết sau khi tất cả các dịch vụ đã được đăng ký. Đây là nơi có thể thực hiện các bước cấu hình thêm cho ứng dụng, như đăng ký các event listener hoặc middleware.


# Routing
 là quá trình xác định cách các yêu cầu HTTP (như GET, POST, PUT, DELETE) được chuyển hướng tới các phần của ứng dụng của bạn. Cụ thể, routing cho phép bạn ánh xạ các URL vào các hàm hoặc phương thức cụ thể trong controller hoặc trả về một phản hồi trực tiếp.
## Cơ bản về Routing
### Định nghĩa Route
Route::get('/hello', function () {
    return 'Hello World';
});
Route sẽ trả về chuỗi "Hello World" khi truy cập URL/hello
### Route với Controller
Route::get('/user/{id}', [UserController::class, 'show']);
### Route Parameters
Route::get('/post/{id}', function ($id) {
    return 'Post ID is '.$id;
});
### Named Routes
Route::get('/profile', [ProfileController::class, 'index'])->name('profile');
### Route Groups
Route::prefix('admin')->group(function () {
    Route::get('/dashboard', function () {
        return 'Admin Dashboard';
    });
});
### Route Middleware
Route::get('/profile', [ProfileController::class, 'index'])->middleware('auth');



# Middleware
là một cơ chế cho phép bạn xử lý và điều chỉnh các yêu cầu HTTP trước khi chúng đến controller hoặc sau khi chúng rời khỏi controller. Middleware giúp bạn thực hiện các nhiệm vụ chung cho tất cả các yêu cầu hoặc nhóm các yêu cầu, chẳng hạn như xác thực, kiểm tra quyền truy cập, xử lý cookie, hoặc thay đổi dữ liệu đầu vào/đầu ra.
## Một số điểm chính
### Tạo Midđleware
php artisan make:middleware CheckAge
### Cấu trúc Middleware
namespace App\Http\Middleware;

use Closure;

class CheckAge
{
    /**
     * Handle an incoming request.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  \Closure  $next
     * @return mixed
     */
    public function handle($request, Closure $next)
    {
        if ($request->age < 18) {
            return redirect('home');
        }

        return $next($request);
    }
}
### Gán Middleware cho Route
Route::get('/profile', [ProfileController::class, 'index'])->middleware('auth');
### Middleware Group
protected $middlewareGroups = [
    'web' => [
        \App\Http\Middleware\EncryptCookies::class,
        \Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class,
        \Illuminate\Session\Middleware\StartSession::class,
        // ... other middleware
    ],
    'api' => [
        'throttle:api',
        \Illuminate\Routing\Middleware\SubstituteBindings::class,
    ],
];
### Global Middleware
protected $middleware = [
    \App\Http\Middleware\TrustProxies::class,
    \Illuminate\Foundation\Http\Middleware\PreventRequestsDuringMaintenance::class,
    \Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class,
    \Illuminate\Session\Middleware\StartSession::class,
    // ... other middleware
];
### Middleware Parameters
public function handle($request, Closure $next, $role)
{
    if (!$request->user()->hasRole($role)) {
        return redirect('home');
    }

    return $next($request);
}



# Controllers
là các lớp chịu trách nhiệm xử lý logic của ứng dụng và điều phối các yêu cầu HTTP từ người dùng. Controllers giúp bạn tổ chức mã nguồn một cách sạch sẽ và có cấu trúc hơn bằng cách tách biệt logic xử lý yêu cầu khỏi các route và views.
## Một số điểm chính







