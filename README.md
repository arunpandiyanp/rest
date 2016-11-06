# rest
rest program
ViewController.h

#import <UIKit/UIKit.h>

@interface ViewController : UIViewController

{
    NSMutableData * mut;
    NSDictionary * dc;
    
}
@end
View Controller .m
#import "ViewController.h"


@interface ViewController ()<NSURLConnectionDelegate>

@end

@implementation ViewController

- (void)viewDidLoad {
    
    NSString *string=@"value=getcountry";
    NSData *postdata=[string dataUsingEncoding: NSASCIIStringEncoding allowLossyConversion:YES];
    NSString *postlenght=[NSString stringWithFormat:@"%lu",(unsigned long)[postdata length]];
    NSLog(@"postdata-->%@,postlenght-->%@",postdata,postlenght);
    NSMutableURLRequest *request=[[NSMutableURLRequest alloc]init];
    [request setURL:[NSURL URLWithString:@"http://onesee.co.uk/ios/api.php?"]];
    [request setHTTPMethod:@"POST"];
    [request setValue:postlenght forHTTPHeaderField:@"ContentLength"];
    [request setHTTPBody:postdata];
    
    NSURLConnection *connection=[[NSURLConnection alloc]initWithRequest:request  delegate:self];
    mut=[NSMutableData data];
    
    [super viewDidLoad];
    // Do any additional setup after loading the view, typically from a nib.
}
- (void)connection:(NSURLConnection *)connection didReceiveResponse:(NSURLResponse *)response;{
    [mut setLength:0];
    NSLog(@"%@response",response);
    
}
- (void)connection:(NSURLConnection *)connection didReceiveData:(NSData *)data;
{
    [mut appendData:data];
}
- (void)connectionDidFinishLoading:(NSURLConnection *)connection;{
    NSDictionary *z1=[[NSMutableDictionary alloc]init];
    z1=[NSJSONSerialization JSONObjectWithData:mut options:NSJSONReadingAllowFragments error:nil];
    NSLog(@"z1-->%@",z1);
    
}

- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

@end
