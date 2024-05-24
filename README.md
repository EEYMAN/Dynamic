# Dynamic
import UIKit

class ViewController: UIViewController {
    
        var squareView = UIView()
        var squareViewAnnchorView = UIView()
        var anchorView = UIView()
        var animator = UIDynamicAnimator()
        var attachmentBehavior: UIAttachmentBehavior?
        
        override func viewDidLoad() {
            super.viewDidLoad()
            
            createGestureRecognizer()
            createSmallSquareView()
            createAnimationAndBehaviors()
            createAnchorView()
        
    }
    
    // Create brown square in green squre
    
    func createSmallSquareView() {
        squareView = UIView(frame: CGRect(x: 0, y: 0, width: 80, height: 80))
        squareView.backgroundColor = UIColor.green
        squareView.center = view.center
        squareViewAnnchorView = UIView(frame: CGRect(x: 60, y: 0, width: 20, height: 20))
        squareViewAnnchorView.backgroundColor = UIColor.brown
        squareView.addSubview(squareViewAnnchorView)
        view.addSubview(squareView)
    }
    
    // Create view anchor point
    func createAnchorView() {
        anchorView = UIView(frame: CGRect(x: 120, y: 120, width: 20, height: 20))
        anchorView.backgroundColor = UIColor.red
        view.addSubview(anchorView)
    }
    
    // Create gesture recorder
    func createGestureRecognizer() {
        let panGestureRecognizer = UIPanGestureRecognizer(target: self, action: #selector(handletPan(paramPan:)))
        view.addGestureRecognizer(panGestureRecognizer)
    }
    
    // Create collision and sticking
    func createAnimationAndBehaviors() {
        animator = UIDynamicAnimator(referenceView: view)
        
    // Create collision
        let collision = UICollisionBehavior(items: [squareView])
        collision.translatesReferenceBoundsIntoBoundary = true
        attachmentBehavior = UIAttachmentBehavior(item: squareView, attachedToAnchor: anchorView.center)
        animator.addBehavior(collision)
        animator.addBehavior(attachmentBehavior!)
    }
    
    // Detects pressing
    @objc func handletPan(paramPan: UIPanGestureRecognizer) {
        let tapPoint = paramPan.location(in: view)
        print(tapPoint)
        attachmentBehavior?.anchorPoint = tapPoint
        anchorView.center = tapPoint
    }
    
    
}
