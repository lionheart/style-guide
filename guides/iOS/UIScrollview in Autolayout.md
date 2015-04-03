[Back to Home](../../README.md)

# UIScrollView in Autolayout

### What we think works

Take the following code which (with the help of [LHSCategoryCollection](https://github.com/lionheart/LHSCategoryCollection)) instantiates both a UIScrollView and UIView then positions them with Autolayout to take up the full width and height of the main view.

```objective-c
#import <LHSCategoryCollection/UIView+LHSAdditions.h>

- (void)viewDidLoad {
    [super viewDidLoad];
    
    self.scrollView = [[UIScrollView alloc] init];
    self.scrollView.translatesAutoresizingMaskIntoConstraints = NO;
    self.scrollView.backgroundColor = [UIColor greenColor];
    [self.view addSubview:self.scrollView];
    
    self.exampleView = [[UIView alloc] init];
    self.exampleView.translatesAutoresizingMaskIntoConstraints = NO;
    self.exampleView.backgroundColor = [UIColor redColor];
    [self.exampleView addSubview:self.exampleView];
    
    [self.scrollView lhs_expandToFillSuperview];
    [self.exampleView lhs_expandToFillSuperview];
}
```

Logically, one would expect to see a red screen when running this code. Instead, we see a green screen, but how can this be?

### The Problem

When using a UIScrollView in Autolayout, the elements inside of the UIScrollview are laid out to match the width of the UIScrollView's `contentSize`. The `contentSize` attribute is determined by the subviews of the UIScrollView, and because we did not give `exampleView` an explicit width, it is given the width of 0 - giving us the green screen in the above example.

### The Solution

In order to circumvent this behaviour, the take the following code:

```objective-c
#import <LHSCategoryCollection/UIView+LHSAdditions.h>

- (void)viewDidLoad {
    [super viewDidLoad];
    
    self.scrollView = [[UIScrollView alloc] init];
    self.scrollView.translatesAutoresizingMaskIntoConstraints = NO;
    self.scrollView.backgroundColor = [UIColor greenColor];
    [self.view addSubview:self.scrollView];
    
    self.contentView = [[UIView alloc] init];
    self.contentView.translatesAutoresizingMaskIntoConstraints = NO;
    [self.scrollView addSubview:self.contentView];
    
    self.exampleView = [[UIView alloc] init];
    self.exampleView.translatesAutoresizingMaskIntoConstraints = NO;
    self.exampleView.backgroundColor = [UIColor redColor];
    [self.contentView addSubview:self.exampleView];
    
    NSDictionary *metrics = @{};
    
    NSDictionary *views = @{
                            @"mainView": self.view,
                            @"contentView": self.contentView};
    
    [self.scrollView lhs_expandToFillSuperview];
    [self.contentView lhs_fillHeightOfSuperview];
    
    [self.view lhs_addConstraints:@"H:|[contentView(==mainView)]|" metrics:metrics views:views];
    
    [self.exampleView lhs_expandToFillSuperview];
    
}
```

What is happening here, is that we are adding `contentView` to `scrollView` and setting its width equivalent to that of the main view. This way we can circumvent the fact that subviews of a UIScrollView have their widths set by the `contentSize` of the UIScrollView (which is determined by the widest element).