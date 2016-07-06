#GameplayKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKAgent.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKAgent.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKAgent.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKAgent.h	2016-05-18 05:10:29.000000000 +0200
@@ -1,18 +1,16 @@
 //
 //  GKAgent.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright © 2014 Apple. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
-#import <simd/simd.h>
+#import <GameplayKit/GameplayKitBase.h>
 
-#import <GameplayKit/GameplayKit.h>
-#import "GKComponent.h"
-#import "GKObstacle.h"
-#import "GKBehavior.h"
-#import "GKGoal.h"
+#import <GameplayKit/GKComponent.h>
+#import <GameplayKit/GKObstacle.h>
+#import <GameplayKit/GKBehavior.h>
+#import <GameplayKit/GKGoal.h>
 
 @class GKAgent, GKBehavior, GKPath;
 
@@ -22,8 +20,8 @@
  * Delegate that will receive messages regarding GKAgent updates.
  */
 @protocol GKAgentDelegate <NSObject>
-@optional
 
+@optional
 /*
  * Called before [GKAgent updateWithDeltaTime:] is called each frame.
  */
@@ -47,7 +45,7 @@
  * these values should be scaled and biased into their target coordinate system and a simple filter on top ensures
  * any noise generated from the steering logic doesn't affect the visual represtentation.
  */
-GK_BASE_AVAILABILITY @interface GKAgent : GKComponent
+GK_BASE_AVAILABILITY @interface GKAgent : GKComponent <NSCoding>
 
 /**
  * Object which has agentDidUpdate called on it during this agent's behavior updatekbeha
@@ -79,7 +77,7 @@
  *
  * Defaults to 0.0
  */
-@property (nonatomic, readonly) float speed;
+@property (nonatomic) float speed;
 
 /**
  * Maximum amount of acceleration that can be applied to this agent.  All applied impulses are clipped to this amount.
@@ -99,12 +97,12 @@
 
 
 /**
- * A 2D specalization of an agent that moves on in a 2-axis logical coordinate system. This coordinate system does not
+ * A 2D specalization of an agent that moves on a 2-axis logical coordinate system. This coordinate system does not
  * need to match the visual coordinate system of the delegate. One simple case of that is isometric 2D content where the
  * game model is on a flat 2D plane but the visuals are displayed on an angle where one of the logical axes are used for
  * simulated depth as well as some translation in the display plane.
  */
-GK_BASE_AVAILABILITY @interface GKAgent2D : GKAgent
+GK_BASE_AVAILABILITY @interface GKAgent2D : GKAgent <NSCoding>
 
 /**
  * Position of the agent on the logical XY plane
@@ -129,4 +127,36 @@
 
 @end
 
+/**
+ * A 3D specialization of an agent that moves on a 3-axis logical coordinate system.
+ */
+GK_BASE_AVAILABILITY @interface GKAgent3D : GKAgent
+
+
+/**
+ * Position of the agent on the logical XYZ plane
+ */
+@property (nonatomic, assign) vector_float3 position;
+
+/**
+ * Current logical velocity of the agent. The forward vector can be derived by normalizing this.
+ */
+@property (nonatomic, readonly) vector_float3 velocity;
+
+
+/**
+ * The 3x3 rotation matrix that defines the orientation of this agent in 3D space
+ * columns[0] is forward, columns[1] is up, columns[2] is side
+ */
+@property (nonatomic, assign) matrix_float3x3 rotation;
+
+
+/**
+ * Overridden from GKComponent.
+ * Updates this agent with the current behavior, generating a force to reach its goals and applying that force.
+ */
+- (void)updateWithDeltaTime:(NSTimeInterval)seconds;
+
+@end
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKBehavior.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKBehavior.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKBehavior.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKBehavior.h	2016-05-25 04:45:23.000000000 +0200
@@ -1,21 +1,21 @@
 //
 //  GKBehavior.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright © 2015 Apple. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
-#import "GameplayKitBase.h"
+#import <GameplayKit/GameplayKitBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 @class GKGoal;
 
 /**
- * A collection of GKGoals and weights that can be applied to a GKAgent
+ * A collection of GKGoals or GKBehaviors with weights that can be applied to a GKAgent
+ * The sub-goals or sub-behaviors are summed to produce a total force to be applied to an agent
  */
-GK_BASE_AVAILABILITY @interface GKBehavior : NSObject<NSFastEnumeration>
+GK_BASE_AVAILABILITY @interface GKBehavior : NSObject<NSFastEnumeration, NSCopying>
 
 /*
  * The number of GKGoals in this behavior
@@ -79,8 +79,8 @@
 /**
  * Supports getting a weight via a [goal] subscript.
  */
-- (NSNumber *)objectForKeyedSubscript:(GKGoal *)goal;
+- (nullable NSNumber *)objectForKeyedSubscript:(GKGoal *)goal;
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKComponent.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKComponent.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKComponent.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKComponent.h	2016-05-25 04:45:23.000000000 +0200
@@ -1,12 +1,11 @@
 //
 //  GKComponent.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright (c) 2014 Apple. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
-#import "GameplayKitBase.h"
+#import <GameplayKit/GameplayKitBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -21,7 +20,7 @@
  
  @see GKComponentSystem
  */
-GK_BASE_AVAILABILITY @interface GKComponent : NSObject <NSCopying>
+GK_BASE_AVAILABILITY @interface GKComponent : NSObject <NSCopying, NSCoding>
 
 /**
  * The entity that this component belongs to. Defaults to nil until the component is added to an entity.
@@ -34,6 +33,16 @@
  */
 - (void)updateWithDeltaTime:(NSTimeInterval)seconds;
 
+/**
+ * Override this to perform game logic when this component is added to an entity
+ */
+-(void)didAddToEntity;
+
+/**
+ * Override this to perform game logic before this entity is removed from it's entity
+ */
+-(void)willRemoveFromEntity;
+
 @end
 
 
@@ -110,6 +119,11 @@
  */
 - (void)updateWithDeltaTime:(NSTimeInterval)seconds;
 
+/**
+ * Returns the class of the specified generic index
+ */
+- (nonnull Class)classForGenericArgumentAtIndex:(NSUInteger)index;
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKCompositeBehavior.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKCompositeBehavior.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKCompositeBehavior.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKCompositeBehavior.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1,76 @@
+//
+//  GKCompositeBehavior.h
+//  GameplayKit
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <GameplayKit/GKBehavior.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*
+ * A GKBehavior that can also contain a number of sub-behaviors
+ * Sub-behaviors and goals are both weighted and produce a force to apply to a GKAGENT
+ */
+@interface GKCompositeBehavior : GKBehavior
+
+/**
+ * Number of sub-behaviors in this behavior
+ **/
+@property (readonly) NSInteger behaviorCount;
+
+/**
+ * Creates a behavior with an array of sub-behaviors
+ */
++ (instancetype)behaviorWithBehaviors:(NSArray<GKBehavior *> *)behaviors;
+
+/**
+ * Creates a behavior with two associated arrays of sub-behaviors and weights
+ */
++ (instancetype)behaviorWithBehaviors:(NSArray<GKBehavior *> *)behaviors andWeights:(NSArray<NSNumber*> *)weights;
+
+
+/**
+ * Adds a new sub-behavior or changes the weight of the existing sub-behavior in this behavior.
+ * If the sub-behavior  does not exist in this behavior, it is added.
+ * @param weight the weight for this goal
+ * @param behavior the sub-behavior who's weight to change
+ */
+- (void)setWeight:(float)weight forBehavior:(GKBehavior *)behavior;
+
+/**
+ * Gets the current weight for a given sub-behavior.
+ * @return the weight of the sub-behavior, or 0 if there is no such sub-behavior on this behavior
+ */
+- (float)weightForBehavior:(GKBehavior *)behavior;
+
+/**
+ * Remove the indicated sub-behavior from this behavior.
+ * @param behavior the sub-behavior to be removed
+ */
+- (void)removeBehavior:(GKBehavior *)behavior;
+
+/**
+ * Removes all the sub-behavior on the behavior.
+ */
+- (void)removeAllBehaviors;
+
+/**
+ * Supports getting behaviors via a [int] subscript.
+ */
+- (GKBehavior *)objectAtIndexedSubscript:(NSUInteger)idx;
+
+/**
+ * Supports setting a weight via a [behavior] subscript.
+ */
+- (void)setObject:(NSNumber *)weight forKeyedSubscript:(GKBehavior *)behavior;
+
+/**
+ * Supports getting a weight via a [behavior] subscript.
+ */
+- (NSNumber *)objectForKeyedSubscript:(GKBehavior *)behavior;
+
+@end
+
+NS_ASSUME_NONNULL_END
\ No newline at end of file
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKDecisionTree.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKDecisionTree.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKDecisionTree.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKDecisionTree.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1,102 @@
+//
+//  GKDecisionTreeStrategist.h
+//  GameplayKit
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <GameplayKit/GameplayKitBase.h>
+#import <GameplayKit/GKRandomSource.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+GK_BASE_AVAILABILITY_2 @interface GKDecisionNode : NSObject
+
+/**
+ * Creates a numeric branch to a node containing the specified attribute
+ *
+ * @param branch The branch of this node for the specified value
+ * @param attribute The attribute of the created node
+ * @return The node lead to by the branch
+ */
+- (instancetype)createBranchWithValue:(NSNumber *)value attribute:(id <NSObject>)attribute;
+
+/**
+ * Creates a predicated branch to a node containing the specified attribute
+ *
+ * @param branch The branch of this node for the provided predicate
+ * @param attribute The attribute of the created node
+ * @return The node lead to by the branch
+ */
+- (instancetype)createBranchWithPredicate:(NSPredicate *)predicate attribute:(id <NSObject>)attribute;
+
+/**
+ * Creates a random branch to a node containing the specified attribute
+ *
+ * @param branch The branch of this node with the given weight (weighted for random selection)
+ * @param attribute The attribute of the created node
+ * @return The node lead to by the branch
+ *
+ * @see GKDecisionTree
+ */
+- (instancetype)createBranchWithWeight:(NSInteger)weight attribute:(id <NSObject>)attribute;
+
+@end
+
+
+GK_BASE_AVAILABILITY_2 @interface GKDecisionTree : NSObject <NSSecureCoding>
+
+/**
+ * The node for the decision tree that all other nodes descend from
+ */
+@property (nonatomic, readonly, nullable) GKDecisionNode *rootNode;
+
+/**
+ * The random source used by the decision tree when descending on a random branch
+ * This must be set before creating any weighted branches
+ * @see GKDecisionNode
+ */
+@property (copy, nonatomic) GKRandomSource *randomSource;
+
+/**
+ * Initializes the decision tree with a root node containing the provided attribute
+ *
+ * @param attribute The attribute to be contained at the root of the tree
+ * @return GKDecisionTree with the set root
+ */
+- (instancetype)initWithAttribute:(id <NSObject>)attribute;
+
+/**
+ * Initializes and constructs a decision tree by learning from the provided examples & attributes
+ *
+ * @param examples Must be an array of examples (with each example being a collection of the various attributes at a given state)
+ * @param results An array of the corresponding results for each example. Ordered such that the first result matches with the first example in examples.
+ * @param attributes The list of attributes. Ordered such that the first attribute matches with the first result in each example.
+ * So if we have two attributes: [distance, jump height], and two examples: [[20, 8], [15, 14]], and the resulting actions here: [Roll, Jump], we can think of this as a matrix:
+ *
+ *          distance| height            <-  Attributes
+ *           _______|_______
+ *          |       |       |
+ *          |  20   |   8   |  jump
+ *          |-------|-------|-------    <-  Results
+ *          |  15   |   14  |  roll
+ *          |_______|_______|
+ *                  ^
+ *                  |
+ *               Examples
+ *
+ * @return GKDecisionTree created by learning from the provided examples for the provided attributes
+ */
+- (instancetype)initWithExamples:(NSArray <NSArray <id <NSObject>>*>*)examples actions:(NSArray <id <NSObject>>*)actions attributes:(NSArray <id <NSObject>>*)attributes;
+
+/**
+ * Will branch down from the root node to find the correct action attribute for the given collection of results and their respective attributes
+ *
+ * @param answers The dictionary of attributes (keys) and their answers (values)
+ * @return The attribute found by traversing the tree given the provided answers
+ */
+- (id <NSObject>)findActionForAnswers:(NSDictionary <id <NSObject>, id <NSObject>>*)answers;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKEntity.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKEntity.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKEntity.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKEntity.h	2016-05-25 04:45:23.000000000 +0200
@@ -1,11 +1,11 @@
 //
 //  GKEntity.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright (c) 2014 Apple. All rights reserved.
 //
 
-#import <GameplayKit/GameplayKit.h>
+#import <GameplayKit/GameplayKitBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -15,12 +15,12 @@
  * An entity is the general purpose object in an entity-component system.
  * Entites have many components but components are associated with only a single entity.
  * 
- * Note: GKEntity supports NSCopying, but your custom GKComponent's must also support NSCopying
+ * Note: GKEntity supports NSCopying and NSCoding, but your custom GKComponent's must also support NSCopying and NSCoding
  *
  * @see GKComponent
  * @see GKComponentSystem
  */
-GK_BASE_AVAILABILITY @interface GKEntity : NSObject <NSCopying>
+GK_BASE_AVAILABILITY @interface GKEntity : NSObject <NSCopying, NSCoding>
 
 /**
  * Creates a new entity ready to have components added to it.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGameModel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGameModel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGameModel.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGameModel.h	2016-05-14 11:24:57.000000000 +0200
@@ -1,11 +1,11 @@
 //
 //  GKGameModel.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright (c) 2014 Apple. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
+#import <GameplayKit/GameplayKitBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGoal.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGoal.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGoal.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGoal.h	2016-05-18 03:51:26.000000000 +0200
@@ -1,12 +1,11 @@
 //
 //  GKGoal.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright © 2015 Apple. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
-#import "GameplayKitBase.h"
+#import <GameplayKit/GameplayKitBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGraph.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGraph.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGraph.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGraph.h	2016-06-21 18:28:24.000000000 +0200
@@ -1,11 +1,11 @@
 //
 //  GKGraph.m
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright (c) 2014 Apple. All rights reserved.
 //
 
-#import "GameplayKit.h"
+#import <GameplayKit/GameplayKitBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -14,7 +14,7 @@
 /**
  * Representation of a directed graph of GKGraphNodes
  */
-GK_BASE_AVAILABILITY @interface GKGraph : NSObject
+GK_BASE_AVAILABILITY @interface GKGraph : NSObject <NSCopying, NSCoding>
 
 /**
  * The list of nodes in this graph
@@ -61,171 +61,4 @@
 
 @end
 
-
-/**
- * A collection of GKGraphNodes that are governed by a set of extruded GKPolygonObstacles
- */
-GK_BASE_AVAILABILITY @interface GKObstacleGraph : GKGraph
-
-/*
- * Array of the extruded obstacles currently represented by this graph
- */
-@property (nonatomic, readonly) NSArray<GKPolygonObstacle *> *obstacles;
-
-/*
- * The distance by which all obstacles are extruded.
- * This is most commonly the spatial bounding radius of a potential traveler on this path
- */
-@property (nonatomic, readonly) float bufferRadius;
-
-/**
- * Creates an optimal bidirectional graph based on a list of obstacles.
- * Each vertex of each obstacle is extruded and a connection is made between each vertex that does not intersect an obstacle
- * Guaranteed not to have any edges which intersect obstacles.
- * Same effect as [[GKObstacleGraph alloc] init], setting bufferRadius, and then calling addObstacles.
- * @param obstacles a list of obstacles to create the graph from
- * @param bufferRadius the circular radius of a potential agent that will navigate this graph.  Obstacles are extruded by this amount to create the graph.  Must be positive.  Negative values are clipped to 0.0f
- */
-+ (instancetype)graphWithObstacles:(NSArray<GKPolygonObstacle *> *)obstacles bufferRadius:(float)bufferRadius;
-- (instancetype)initWithObstacles:(NSArray<GKPolygonObstacle *> *)obstacles  bufferRadius:(float)bufferRadius;
-
-
-/**
- * Connects the node to this graph by testing edge intersection with existing obstacles.
- * Same behavior as if this node had been present during initWithObstacles.
- * @param node the node to connect
- */
-- (void)connectNodeUsingObstacles:(GKGraphNode2D *)node;
-
-/**
- * Same behavior as connectNodeUsingObstacles: except you can optionally ignore certain obstacles from being tested for intersection.
- */
-- (void)connectNodeUsingObstacles:(GKGraphNode2D *)node ignoringObstacles:(NSArray<GKPolygonObstacle *> *)obstaclesToIgnore;
-
-/**
- * Same behavior as connectNodeUsingObstacles: except you can optionally ignore the bounding radius of certain obstacles from being tested for intersection
- */
-- (void)connectNodeUsingObstacles:(GKGraphNode2D *)node ignoringBufferRadiusOfObstacles:(NSArray<GKPolygonObstacle *> *)obstaclesBufferRadiusToIgnore;
-
-/**
- * Adds obstacles to this graph.
- * Obstacle is extruded and graph nodes are generated from its vertices and then connected to this graph
- * Nothing is done if an obstacle is already present in this graph
- * Any existing connections that intersect the new obstacles are destroyed unless they are protected with [GKObstacleGraph lockConnection:]
- * @param obstacles an array of obstacles to be added
- * @see lockConnection
- */
-- (void)addObstacles:(NSArray<GKPolygonObstacle *> *)obstacles;
-
-/**
- * Removes obstacles from this graph.
- * All associated graph nodes are removed and their connections are bidirectionally removed.
- * Connections between obstacle nodes that were previously invalidated by any of these obstacles are restored.
- * Nothing is done if an obstacle is already present in this graph
- * @param obstacles an array of obstacles to be removed
- */
-- (void)removeObstacles:(NSArray<GKPolygonObstacle *> *) obstacles;
-
-/**
- * Removes all obstacles from this graph.
- */
-- (void)removeAllObstacles;
-
-/**
- * Returns an array of the graph nodes associated with a given obstacle
- * @param obstacle the obstacle who's nodes are to be retrieved
- */
--(NSArray<GKGraphNode2D *> *)nodesForObstacle:(GKPolygonObstacle *)obstacle;
-
-/**
- * Marks a connection as "locked", preventing this connection from being destroyed when you add obstacles that would intersect it
- * @param startNode startNode of the connection to lock
- * @param endNode endNode of the connection to lock
- */
-- (void)lockConnectionFromNode:(GKGraphNode2D *)startNode toNode:(GKGraphNode2D *)endNode;
-
-/**
- * "Unlocks" a connection, removing its protection from being destroyed when you add obstacles that would intersect it
- * @param startNode startNode of the connection to unlock
- * @param endNode endNode of the connection to unlock
- * @see lockConnection
- */
-- (void)unlockConnectionFromNode:(GKGraphNode2D *)startNode toNode:(GKGraphNode2D *)endNode;
-
-/**
- * Query if a given connection is locked
- * @param startNode startNode of the connection to query
- * @param endNode endNode of the connection to query
- * @see lockConnection
- * @see unlockConnection
- * @return YES if the connection was locked with lockConnection, NO if it was never locked or was unlocked via unlockConnection
- */
-- (BOOL)isConnectionLockedFromNode:(GKGraphNode2D *)startNode toNode:(GKGraphNode2D *)endNode;
-
-@end
-
-
-
-/*
- * A collection of GKGraphNodes that are governed by a 2D Cartesian grid
- */
-GK_BASE_AVAILABILITY @interface GKGridGraph : GKGraph
-
-/*
- * The minimum X and Y coordinates of the 2D Cartesian grid this graph represents
- */
-@property (nonatomic, readonly) vector_int2 gridOrigin;
-
-/*
- * The width of the 2D Cartesian grid this graph represents
- */
-@property (nonatomic, readonly) NSUInteger gridWidth;
-
-/*
- * The height of the 2D Cartesian grid this graph represents
- */
-@property (nonatomic, readonly) NSUInteger gridHeight;
-
-/*
- * Returns YES if this grid is also connected via it's diagonal directions rather than only it's cardinal directions
- */
-@property (nonatomic, readonly) BOOL diagonalsAllowed;
-
-/**
- * Creates a bidirectional graph connecting all of the points on a 2D grid
- * @param x starting x value of the grid
- * @param y starting y value of the grid
- * @param width how wide the grid will be; the grid will continue along the positive X axis from the starting x value
- * @param height how high the grid will be; the grid will continue along the positive Y axis from the starting y value
- * @param diagonalsAllowed should diagonal connections between nodes be made?  If not, only cardinal directions will be connected.
- */
-+ (instancetype)graphFromGridStartingAt:(vector_int2)position width:(int)width height:(int)height diagonalsAllowed:(BOOL)diagonalsAllowed;
-
-/**
- * Creates a bidirectional graph connecting all of the points on a 2D grid
- * @param x starting x value of the grid
- * @param y starting y value of the grid
- * @param width how wide the grid will be; the grid will continue along the positive X axis from the starting x value
- * @param height how high the grid will be; the grid will continue along the positive Y axis from the starting y value
- * @param diagonalsAllowed should diagonal connections between nodes be made?  If not, only cardinal directions will be connected.
- */
-- (instancetype)initFromGridStartingAt:(vector_int2)position width:(int)width height:(int)height diagonalsAllowed:(BOOL)diagonalsAllowed;
-
-/**
- * Returns the GKGridGraphNode at the indicated X and Y coordinate
- * Returns nil if it is outside the bounds of minCoordinates and maxCoordinates
- * @param x x coordinate of the grid node to return
- * @param y y coordinate of the grid node to return
- */
-- (nullable GKGridGraphNode *)nodeAtGridPosition:(vector_int2)position;
-
-/**
- * Connects the given GKGridGraphNode to this graph by connecting it to it's adjacent nodes on the grid
- * Input node must have coordinates within the rectangle specified by minCoordinates and maxCoordinates
- * @param node the node to be connected
- */
-- (void)connectNodeToAdjacentNodes:(GKGridGraphNode *)node;
-
-@end
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGraphNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGraphNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGraphNode.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGraphNode.h	2016-05-25 04:45:23.000000000 +0200
@@ -1,19 +1,18 @@
 //
 //  GKGraph.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright (c) 2014 Apple. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
-#import "GameplayKit.h"
+#import <GameplayKit/GameplayKitBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 /**
  * A node in a directed graph. Edges are directed and can have variable costs.
  */
-GK_BASE_AVAILABILITY @interface GKGraphNode : NSObject
+GK_BASE_AVAILABILITY @interface GKGraphNode : NSObject <NSCoding>
 
 /**
  * List of other graph nodes that this node has an edge leading to.
@@ -72,20 +71,31 @@
 @property (nonatomic) vector_float2 position;
 
 + (instancetype)nodeWithPoint:(vector_float2)point;
-- (instancetype)initWithPoint:(vector_float2)point NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithPoint:(vector_float2)point;
 
 @end
 
+/**
+ * GKGraphNode coupled with a 3D position
+ */
+GK_BASE_AVAILABILITY @interface GKGraphNode3D : GKGraphNode
+
+@property (nonatomic) vector_float3 position;
+
++ (instancetype)nodeWithPoint:(vector_float3)point;
+- (instancetype)initWithPoint:(vector_float3)point;
+
+@end
 
 /**
  * GKGraphNode coupled with a position on a 2D grid
  */
 GK_BASE_AVAILABILITY @interface GKGridGraphNode : GKGraphNode
 
-@property (nonatomic) vector_int2 gridPosition;
+@property (nonatomic, readonly) vector_int2 gridPosition;
 
 + (instancetype)nodeWithGridPosition:(vector_int2)gridPosition;
-- (instancetype)initWithGridPosition:(vector_int2)gridPosition NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithGridPosition:(vector_int2)gridPosition;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGridGraph.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGridGraph.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGridGraph.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGridGraph.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1,85 @@
+//
+//  GKGridGraph.h
+//  GameplayKit
+//
+//  Copyright © 2015 Apple. All rights reserved.
+//
+
+#include <GameplayKit/GKGraph.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+
+@class GKGridGraphNode;
+
+/*
+ * A collection of GKGraphNodes that are governed by a 2D Cartesian grid
+ */
+GK_BASE_AVAILABILITY @interface GKGridGraph<NodeType : GKGridGraphNode *>  : GKGraph
+
+/*
+ * The minimum X and Y coordinates of the 2D Cartesian grid this graph represents
+ */
+@property (nonatomic, readonly) vector_int2 gridOrigin;
+
+/*
+ * The width of the 2D Cartesian grid this graph represents
+ */
+@property (nonatomic, readonly) NSUInteger gridWidth;
+
+/*
+ * The height of the 2D Cartesian grid this graph represents
+ */
+@property (nonatomic, readonly) NSUInteger gridHeight;
+
+/*
+ * Returns YES if this grid is also connected via it's diagonal directions rather than only it's cardinal directions
+ */
+@property (nonatomic, readonly) BOOL diagonalsAllowed;
+
+/**
+ * Creates a bidirectional graph connecting all of the points on a 2D grid
+ * @param x starting x value of the grid
+ * @param y starting y value of the grid
+ * @param width how wide the grid will be; the grid will continue along the positive X axis from the starting x value
+ * @param height how high the grid will be; the grid will continue along the positive Y axis from the starting y value
+ * @param diagonalsAllowed should diagonal connections between nodes be made?  If not, only cardinal directions will be connected.
+ */
++ (instancetype)graphFromGridStartingAt:(vector_int2)position width:(int)width height:(int)height diagonalsAllowed:(BOOL)diagonalsAllowed;
+- (instancetype)initFromGridStartingAt:(vector_int2)position width:(int)width height:(int)height diagonalsAllowed:(BOOL)diagonalsAllowed;
+
+/**
+ * Creates a bidirectional graph connecting all of the points on a 2D grid
+ * @param x starting x value of the grid
+ * @param y starting y value of the grid
+ * @param width how wide the grid will be; the grid will continue along the positive X axis from the starting x value
+ * @param height how high the grid will be; the grid will continue along the positive Y axis from the starting y value
+ * @param diagonalsAllowed should diagonal connections between nodes be made?  If not, only cardinal directions will be connected.
+ * @param nodeClass the class of the nodes that this graph should create.  Must descend from GKGridGraphNode
+ */
++ (instancetype)graphFromGridStartingAt:(vector_int2)position width:(int)width height:(int)height diagonalsAllowed:(BOOL)diagonalsAllowed nodeClass:(Class)nodeClass;
+- (instancetype)initFromGridStartingAt:(vector_int2)position width:(int)width height:(int)height diagonalsAllowed:(BOOL)diagonalsAllowed nodeClass:(Class)nodeClass;
+
+/**
+ * Returns the GKGridGraphNode at the indicated X and Y coordinate
+ * Returns nil if it is outside the bounds of minCoordinates and maxCoordinates
+ * @param x x coordinate of the grid node to return
+ * @param y y coordinate of the grid node to return
+ */
+- (nullable NodeType)nodeAtGridPosition:(vector_int2)position;
+
+/**
+ * Connects the given GKGridGraphNode to this graph by connecting it to it's adjacent nodes on the grid
+ * Input node must have coordinates within the rectangle specified by minCoordinates and maxCoordinates
+ * @param node the node to be connected
+ */
+- (void)connectNodeToAdjacentNodes:(GKGridGraphNode *)node;
+
+/**
+ * Returns the class of the specified generic index
+ */
+- (nonnull Class)classForGenericArgumentAtIndex:(NSUInteger)index;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKMeshGraph.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKMeshGraph.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKMeshGraph.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKMeshGraph.h	2016-05-25 04:46:26.000000000 +0200
@@ -0,0 +1,112 @@
+//
+//  GKMeshGraph.h
+//  GameplayKit
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <GameplayKit/GKGraph.h>
+#import <GameplayKit/GKPrimitives.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/** Adjusts how graph nodes are created when you triangulate a GKMeshGrapk
+ 
+ @enum GKMeshGraphTriangulationModeVertices Graph nodes will be made at all triangle vertices
+ @enum GKMeshGraphTriangulationModeCenters Graph nodes will be made at all triangle centers
+ @enum GKMeshGraphTriangulationModeEdgeMidpoints Graph nodes will be made at midpoint of all triangle edges
+ */
+typedef NS_OPTIONS(NSUInteger, GKMeshGraphTriangulationMode) {
+    GKMeshGraphTriangulationModeVertices = 1 << 0,
+    GKMeshGraphTriangulationModeCenters = 1 << 1,
+    GKMeshGraphTriangulationModeEdgeMidpoints = 1 << 2
+};
+
+/**
+ * A collection of GKGraphNodes that are governed by a mesh formed by the space between a set of GKPolygonObstacles
+ */
+GK_BASE_AVAILABILITY_2 @interface GKMeshGraph<NodeType : GKGraphNode2D*> : GKGraph
+
+/**
+ *  Array of the extruded obstacles currently represented by this graph
+ */
+@property (nonatomic, readonly, nonnull) NSArray<GKPolygonObstacle *> *obstacles;
+
+/**
+ * The distance by which all obstacles are extruded.
+ * This is most commonly the spatial bounding radius of a potential traveler on this path 
+ */
+@property (nonatomic, readonly) float bufferRadius;
+
+/**
+ * Specifies how graph nodes are generated when you triangulate this graph.
+ * You can combine triangulation modes using the | (OR) operator
+ *
+ * @see GKMeshGraphTriangulationMode
+ */
+@property (nonatomic) GKMeshGraphTriangulationMode triangulationMode;
+
+/**
+ * The number of triangles currently in this mesh graph
+ */
+@property (nonatomic, readonly) NSUInteger triangleCount;
+
+/**
+ * Creates a graph with a given buffer radius
+ * Obstacles can then be added to this graph prior to a call to [GKMeshGraph trianglulate]
+ * @param bufferRadius the circular radius of a potential agent that will navigate this graph.  Obstacles are extruded by this amount to create the graph.  Must be positive.  Negative values are clipped to 0.0f
+ * @param minCoordinate the minimum coordinate (lower left corner) of the bounding box that will encapsulate this graph.  No obstacles should fall outside this bounding box.
+ * @param maxCoordinate the maximum coordinate (upper right corner) of the bounding box that will encapsulate this graph.  No obstacles should fall outside this bounding box.
+ * @param nodeClass the class of the nodes that this graph should create.  Must descend from GKGraphNode2D
+ */
++ (instancetype)graphWithBufferRadius:(float)bufferRadius minCoordinate:(vector_float2)min maxCoordinate:(vector_float2)max nodeClass:(Class)nodeClass;
+- (instancetype)initWithBufferRadius:(float)bufferRadius minCoordinate:(vector_float2)min maxCoordinate:(vector_float2)max nodeClass:(Class)nodeClass;
+
+/**
+ * Same as [GKMeshGraph graphWithBufferRadius:minCoordinate:maxCoordinate:nodeClass:] where custom node class defaults to GKGraphNode2D
+ */
++ (instancetype)graphWithBufferRadius:(float)bufferRadius minCoordinate:(vector_float2)min maxCoordinate:(vector_float2)max;
+- (instancetype)initWithBufferRadius:(float)bufferRadius minCoordinate:(vector_float2)min maxCoordinate:(vector_float2)max;
+
+/**
+ * Adds obstacles to this mesh graph.  Only reflected after the next triangulate call.
+ */
+-(void)addObstacles:(NSArray<GKPolygonObstacle*>*)obstacles;
+
+/**
+ * Removes obstacles from this graph.  Only reflected after the next triangulate call.
+ */
+-(void)removeObstacles:(NSArray<GKPolygonObstacle*>*)obstacles;
+
+/**
+ * Connects the node to this graph by inserting it into an existing triangle and making the appropriate connections
+ * Node must be in the space defined by the min and max coordinates of this graph.
+ * @param node the node to connect
+ */
+- (void)connectNodeUsingObstacles:(NodeType)node;
+
+/**
+ * Generates a new triangle mesh for the given obstacles.  
+ * This should be called after some number of calls to addObstacle
+ * The negative space between all input obstacles are triangulated to create a mesh
+ * This mesh is turned into a set of connected graph nodes based on
+ */
+-(void)triangulate;
+
+
+/**
+ * Returns the triangle at the given index
+ * @see numTriangles
+ * @param index the index of the triangle to be returned
+ * @return the triangle at the given index
+ */
+-(GKTriangle)triangleAtIndex:(NSUInteger)index;
+
+/**
+ * Returns the class of the specified generic index
+ */
+- (nonnull Class)classForGenericArgumentAtIndex:(NSUInteger)index;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKMinmaxStrategist.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKMinmaxStrategist.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKMinmaxStrategist.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKMinmaxStrategist.h	2016-05-25 04:45:23.000000000 +0200
@@ -1,6 +1,6 @@
 //
 //  GKMinmaxStrategist.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright (c) 2014 Apple. All rights reserved.
 //
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKMonteCarloStrategist.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKMonteCarloStrategist.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKMonteCarloStrategist.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKMonteCarloStrategist.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1,33 @@
+//
+//  GKMonteCarloStrategist.h
+//  GameplayKit
+//
+//  Copyright © 2015 Apple. All rights reserved.
+//
+
+#import <GameplayKit/GKStrategist.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/**
+ * The Monte Carlo Strategist is a generic AI that selects a game model update for a given player that results
+ * in the highest likelihood for that player to eventually win the game. It does this by sampling the updates available
+ * to the player in question. In doing this it will select the update it knows to produce the best result so far, expanding on this
+ * selection, simulating the rest of the game from that expansion, and then propogating the results (win or loss) upwards.
+ * It will do this until the budget has been reached, then returning the choice it has deemed best suited for the player in question.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKMonteCarloStrategist : NSObject <GKStrategist>
+
+/**
+ * The maximum number of samples that will be processed when searching for a move.
+ */
+@property (nonatomic, assign) NSUInteger budget;
+
+/**
+ * A weight that encourages exploration of less visited updates versus the continued exploitation of previously visited updates.
+ */
+@property (nonatomic, assign) NSUInteger explorationParameter;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoise.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoise.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoise.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoise.h	2016-05-18 05:10:29.000000000 +0200
@@ -0,0 +1,199 @@
+//
+//  GKNoise.h
+//  GameplayKit
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <GameplayKit/GameplayKitBase.h>
+#import <SpriteKit/SpriteKitBase.h>
+
+@class GKNoiseSource;
+
+NS_ASSUME_NONNULL_BEGIN
+
+/**
+ * GKNoise is the object used to manipulate and combine noise in continuous 3D space.  It takes a GKNoiseSource as input.
+ * To extract and use a portion of the noise within the 3D space use the GKNoiseMap class.
+ *
+ * @see GKNoiseSource
+ * @see GKNoiseMap
+ */
+GK_BASE_AVAILABILITY_2 @interface GKNoise : NSObject
+
+/**
+ * Color gradient of this noise, represented as 'value : color' pairs.  Utilized when this noise is rendered to a texture.
+ */
+@property (nonatomic, copy) NSDictionary<NSNumber *, SKColor *> *gradientColors;
+
+/**
+ * Initializes a constant noise of 0.0 at all positions.
+ */
+- (instancetype)init;
+
+/**
+ * Initializes a noise with the specified noise source.
+ *
+ * @param noiseSource The noise source to use to initially populate the 3D noise space.
+ */
++ (instancetype)noiseWithNoiseSource:(GKNoiseSource *)noiseSource;
+
+/**
+ * Initializes a noise with the specified noise source and parameters.
+ *
+ * @param noiseSource The noise source to use to initially populate the 3D noise space.
+ * @param gradientColors The color gradient to use for this noise in 'value : color' pairs.
+ */
++ (instancetype)noiseWithNoiseSource:(GKNoiseSource *)noiseSource gradientColors:(NSDictionary<NSNumber *, SKColor *> *)gradientColors;
+
+/**
+ * Initializes a noise with the specified noise source.
+ *
+ * @param noiseSource The noise source to use to initially populate the 3D noise space.
+ */
+- (instancetype)initWithNoiseSource:(GKNoiseSource *)noiseSource;
+
+/**
+ * Initializes a noise with the specified noise source and parameters.
+ *
+ * @param noiseSource The noise source to use to initially populate the 3D noise space.
+ * @param gradientColors The color gradient to use for this noise in 'value : color' pairs.
+ */
+- (instancetype)initWithNoiseSource:(GKNoiseSource *)noiseSource gradientColors:(NSDictionary<NSNumber *, SKColor *> *)gradientColors NS_DESIGNATED_INITIALIZER;
+
+/**
+ * Initializes a composite noise from one or more component noises.  Useful for combining and layering noises together.
+ *
+ * @param noises The component noises to combine.
+ * @param selectionNoise The noise that governs which component noise is chosen for each position of the resulting noise.
+ * The range of values is equally-subdivided for each component noise.
+ */
++ (instancetype)noiseWithComponentNoises:(NSArray<GKNoise *> *)noises selectionNoise:(GKNoise *)selectionNoise;
+
+/**
+ * Initializes a composite noise from one or more component noises.  Useful for combining and layering noises together.
+ *
+ * @param noises The component noises to combine.
+ * @param selectionNoise The noise that governs which component noise is chosen for each position of the resulting noise.
+ * The range of values is equally-subdivided for each component noise.
+ * @param componentBoundaries The noise value boundaries of the selection noise to use for the component noises.  Specify
+ * one less boundary than the number of component noises.  This is a parallel array to blendDistances.
+ * @param blendDistances The size of smoothing that is applied to boundaries where two component noises meet.  Specify
+ * one less blend distance than the number of component noises.  This is a parallel array to componentBoundaries.
+ */
++ (instancetype)noiseWithComponentNoises:(NSArray<GKNoise *> *)noises selectionNoise:(GKNoise *)selectionNoise componentBoundaries:(NSArray<NSNumber *> *)componentBoundaries boundaryBlendDistances:(NSArray<NSNumber *> *)blendDistances;
+
+/**
+ * Takes the absoltue value of all noise positions.
+ */
+- (void)applyAbsoluteValue;
+
+/**
+ * Clamps all noise values to the specified bounds.
+ *
+ * @param lowerBound The noise value lower bound.
+ * @param upperBound The noise value upper bound.
+ */
+- (void)clampWithLowerBound:(double)lowerBound upperBound:(double)upperBound;
+
+/**
+ * Raises all noise values to the specified power.
+ *
+ * @param power The power to which to raise all noise values.
+ */
+- (void)raiseToPower:(double)power;
+
+/**
+ * Inverts all noise values, from positive to negative and vice versa.
+ */
+- (void)invert;
+
+/**
+ * Applies a turbulent displacement to all noise values.
+ */
+- (void)applyTurbulenceWithFrequency:(double)frequency power:(double)power roughness:(int)roughness seed:(int32_t)seed;
+
+/**
+ * Remaps all noise values to a smooth curve that passes through the specified control points.
+ *
+ * @param controlPoints Pairs of 'input : output' values to use as control points for the smooth remapping curve.
+ * Duplicate input values are not permitted.
+ */
+- (void)remapValuesToCurveWithControlPoints:(NSDictionary<NSNumber *, NSNumber *> *)controlPoints;
+
+/**
+ * Remaps all noise values to one or more terraces with peaks.  Useful for creating valleys and trenches.
+ *
+ * @param peakInputValues Inputs positions of terrace peaks.
+ * @param inverted Governs the curve direction from peak to peak.
+ */
+- (void)remapValuesToTerracesWithPeaks:(NSArray<NSNumber *> *)peakInputValues terracesInverted:(BOOL)inverted;
+
+/**
+ * Translates all noise values by the specified amount.
+ *
+ * @param delta The amount by which to move all noise values.
+ */
+- (void)moveBy:(vector_double3)delta;
+
+/**
+ * Scales all noise values by the specified amount.
+ *
+ * @param factor The factor by which to scale all noise values.
+ */
+- (void)scaleBy:(vector_double3)factor;
+
+/**
+ * Rotates all noise values by the specified amount.
+ *
+ * @param radians The number of radians in x-, y- and z-axes by which to rotate all noise values.
+ */
+- (void)rotateBy:(vector_double3)radians;
+
+/**
+ * Adds all noise values by the noise values at the same position in specified noise.
+ *
+ * @param noise The noise from which to add values to this noise.
+ */
+- (void)addWithNoise:(GKNoise *)noise;
+
+/**
+ * Multiplies all noise values by the noise values at the same position in specified noise.
+ *
+ * @param noise The noise from which to multiply values to this noise.
+ */
+- (void)multiplyWithNoise:(GKNoise *)noise;
+
+/**
+ * Takes the minimum value between this noise and the specified noise at each position.
+ *
+ * @param noise The noise to compare against this noise at each position in determining which to take the minimum value from.
+ */
+- (void)minimumWithNoise:(GKNoise *)noise;
+
+/**
+ * Takes the maximum value between this noise and the specified noise at each position.
+ *
+ * @param noise The noise to compare against this noise at each position in determining which to take the maximum value from.
+ */
+- (void)maximumWithNoise:(GKNoise *)noise;
+
+/**
+ * Raises all noise values to the power of the value at the same position of the specified noise.
+ *
+ * @param noise The noise from which to raise this noise's values by.
+ */
+- (void)raiseToPowerWithNoise:(GKNoise *)noise;
+
+/**
+ * Displaces all noise values by the values at the same positions of the specified noises.
+ *
+ * @param xDisplacementNoise The noise from which to displace along the x-axis this noise's values at the same positions.
+ * @param yDisplacementNoise The noise from which to displace along the y-axis this noise's values at the same positions.
+ * @param zDisplacementNoise The noise from which to displace along the z-axis this noise's values at the same positions.
+ */
+- (void)displaceXWithNoise:(GKNoise *)xDisplacementNoise yWithNoise:(GKNoise *)yDisplacementNoise zWithNoise:(GKNoise *)zDisplacementNoise;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoiseMap.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoiseMap.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoiseMap.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoiseMap.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1,131 @@
+//
+//  GKNoiseMap.h
+//  GameplayKit
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <GameplayKit/GameplayKitBase.h>
+
+@class GKNoiseSource;
+@class GKNoise;
+
+NS_ASSUME_NONNULL_BEGIN
+
+/**
+ * GKNoiseMap represents an extracted portion of sampled points from continuous 3D noise.  Extracted values are useful
+ * for 2D and 3D games.  Noise values may be queried, set to explicit values or used as input for other uses,
+ * including textures and tile maps.
+ *
+ * @see GKNoiseSource
+ * @see GKNoise
+ * @see SKTexture
+ * @see SKTileMapNode
+ */
+GK_BASE_AVAILABILITY_2 @interface GKNoiseMap : NSObject
+
+/**
+ * The size of the 2D plane to extract from the 3D noise space, in noise space coordinates.  Used together
+ * with origin to determine the bounds of the extracted plane.  A smaller size captures a more "zoomed in"
+ * view of the noise, and vice versa.
+ *
+ * @see origin
+ */
+@property (nonatomic, readonly) vector_double2 size;
+
+/**
+ * The origin of the 2D plane to extract from the 3D noise space, in noise space coordinates.  Used together
+ * with size to determine the bounds of the extracted plane.
+ *
+ * @see size
+ */
+@property (nonatomic, readonly) vector_double2 origin;
+
+/**
+ * The number of equally-spaced samples to make across the 2D plane.  A higher number of samples produces finer
+ * resolution at the expense of increased memory.
+ */
+@property (nonatomic, readonly) vector_int2 sampleCount;
+
+/**
+ * Whether the values at the edges of the 2D plane are modified to allow seamless tiling of the extracted noise map.
+ */
+@property (nonatomic, readonly, getter=isSeamless) BOOL seamless;
+
+/**
+ * Initializes a noise map with constant noise of 0.0 at all positions.
+ */
+- (instancetype)init;
+
+/**
+ * Initializes a noise map with specified noise.
+ *
+ * @param noise The 3D noise from which to sample a 2D plane.
+ */
++ (instancetype)noiseMapWithNoise:(GKNoise *)noise;
+
+/**
+ * Initializes a noise map with specified noise and parameters.
+ *
+ * @param noise The 3D noise from which to sample a 2D plane.
+ * @param size The size of the 2D plane to extract from the 3D noise space, in noise space coordinates.
+ * @param origin The origin of the 2D plane to extract from the 3D noise space, in noise space coordinates.
+ * @param sampleCount The number of equally-spaced samples to make across the 2D plane.
+ * @param seamless Whether the values at the edges of the 2D plane are modified to allow seamless tiling of the extracted noise map.
+ */
++ (instancetype)noiseMapWithNoise:(GKNoise *)noise size:(vector_double2)size origin:(vector_double2)origin sampleCount:(vector_int2)sampleCount seamless:(BOOL)seamless;
+
+/**
+ * Initializes a noise map with specified noise.
+ *
+ * @param noise The 3D noise from which to sample a 2D plane.
+ */
+- (instancetype)initWithNoise:(GKNoise *)noise;
+
+/**
+ * Initializes a noise map with specified noise and parameters.
+ *
+ * @param noise The 3D noise from which to sample a 2D plane.
+ * @param size The size of the 2D plane to extract from the 3D noise space, in noise space coordinates.
+ * @param origin The origin of the 2D plane to extract from the 3D noise space, in noise space coordinates.
+ * @param sampleCount The number of equally-spaced samples to make across the 2D plane.
+ * @param seamless Whether the values at the edges of the 2D plane are modified to allow seamless tiling of the extracted noise map.
+ */
+- (instancetype)initWithNoise:(GKNoise *)noise size:(vector_double2)size origin:(vector_double2)origin sampleCount:(vector_int2)sampleCount seamless:(BOOL)seamless NS_DESIGNATED_INITIALIZER;
+
+/**
+ * The noise map value at the specified sample index of the 2D plane.
+ *
+ * @param position Sample index of the extracted 2D plane at which to query the value.  Valid range
+ * is from 0 to sampleCount-1, inclusive.
+ *
+ * @return The noise map value at the specified sample index.
+ */
+- (float)valueAtPosition:(vector_int2)position;
+
+/**
+ * The noise map value at the specified sample point of the 2D plane.  Returns an interpolated value for
+ * points not aligned on integer boundaries.
+ *
+ * @param position Sample point of the extracted 2D plane at which to query the value.  Valid range
+ * is from 0.0 to sampleCount-1.0, inclusive.
+ *
+ * @return The noise map value at the specified sample index. Returns an interpolated value for points not
+ * aligned on integer boundaries.
+ */
+- (float)interpolatedValueAtPosition:(vector_float2)position;
+
+/**
+ * Sets the specified value to the noise map at the specified sample index of the 2D plane.
+ *
+ * @param value The noise map value to assign to the specified position.
+ * @param position Sample index of the extracted 2D plane at which to set the value.  Valid range
+ * is from 0 to sampleCount-1, inclusive.
+ *
+ * @return The noise map value at the specified sample index.
+ */
+- (void)setValue:(float)value atPosition:(vector_int2)position;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoiseSource.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoiseSource.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoiseSource.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoiseSource.h	2016-05-14 11:24:57.000000000 +0200
@@ -0,0 +1,142 @@
+//
+//  GKNoiseSource.h
+//  GameplayKit
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <GameplayKit/GameplayKitBase.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/**
+ * A GKNoiseSource instance is a description of procedural noise in 3D space.  Noise sources generate values
+ * between -1.0 and 1.0, inclusive, for any position in continuous 3D space.
+ * Subclasses represent specific types of noise, each with their own parameters that affect the nature of the noise.
+ * Noise sources are the starting point for generating and using procedural noise.  The 3D noise values may be manipulated and
+ * combined with the GKNoise class.  Portions of this 3D noise can be extracted and utilized via the GKNoiseMap class.
+ * Extracted portions of noise are useful in both 2D and 3D games.  Applications include creating realistic textures,
+ * height maps for 2D and 3D game world terrain, tile maps for 2D games, and intentionally imperfect game object and
+ * camera movements in 2D and 3D games.
+ * This class is not intended to be instantiated.
+ *
+ * @see GKNoise
+ * @see GKNoiseMap
+ */
+GK_BASE_AVAILABILITY_2 @interface GKNoiseSource : NSObject
+
+@end
+
+/**
+ * Coherent noise is smoothly-changing, semi-random noise.  A given input always produces the same output.
+ * A small change in input produces a small change in output.  A large change in input produces a random
+ * change in output. This class is not intended to be instantiated.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKCoherentNoiseSource : GKNoiseSource
+
+@property (nonatomic) double frequency;
+@property (nonatomic) NSInteger octaveCount;
+@property (nonatomic) double lacunarity;
+@property (nonatomic) int32_t seed;
+
+@end
+
+/**
+ * Perlin noise is useful for creating natural-looking textures and realistic-looking terrain.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKPerlinNoiseSource : GKCoherentNoiseSource
+
+@property (nonatomic) double persistence;
+
++ (instancetype)perlinNoiseSourceWithFrequency:(double)frequency octaveCount:(NSInteger)octaveCount persistence:(double)persistence lacunarity:(double)lacunarity seed:(int32_t)seed;
+- (instancetype)initWithFrequency:(double)frequency octaveCount:(NSInteger)octaveCount persistence:(double)persistence lacunarity:(double)lacunarity seed:(int32_t)seed NS_DESIGNATED_INITIALIZER;
+
+@end
+
+/**
+ * Billow noise is similar to Perlin noise, with more rounded shapes and clearly-defined transitions beween values.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKBillowNoiseSource : GKCoherentNoiseSource
+
+@property (nonatomic) double persistence;
+
++ (instancetype)billowNoiseSourceWithFrequency:(double)frequency octaveCount:(NSInteger)octaveCount persistence:(double)persistence lacunarity:(double)lacunarity seed:(int32_t)seed;
+- (instancetype)initWithFrequency:(double)frequency octaveCount:(NSInteger)octaveCount persistence:(double)persistence lacunarity:(double)lacunarity seed:(int32_t)seed NS_DESIGNATED_INITIALIZER;
+
+@end
+
+/**
+ * Ridged noise is similar to Perlin noise, with sharply-defined, relatively thin peaks.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKRidgedNoiseSource : GKCoherentNoiseSource
+
++ (instancetype)ridgedNoiseSourceWithFrequency:(double)frequency octaveCount:(NSInteger)octaveCount lacunarity:(double)lacunarity seed:(int32_t)seed;
+- (instancetype)initWithFrequency:(double)frequency octaveCount:(NSInteger)octaveCount lacunarity:(double)lacunarity seed:(int32_t)seed NS_DESIGNATED_INITIALIZER;
+
+@end
+
+/**
+ * Voronoi noise partitions the space into angular, polygonal "cells", which are reminiscent
+ * of stained glass or crystal-like structures.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKVoronoiNoiseSource : GKNoiseSource
+
+@property (nonatomic) double frequency;
+@property (nonatomic) double displacement;
+@property (nonatomic, getter=isDistanceEnabled) BOOL distanceEnabled;
+@property (nonatomic) int32_t seed;
+
++ (instancetype)voronoiNoiseWithFrequency:(double)frequency displacement:(double)displacement distanceEnabled:(BOOL)distanceEnabled seed:(int32_t)seed;
+- (instancetype)initWithFrequency:(double)frequency displacement:(double)displacement distanceEnabled:(BOOL)distanceEnabled seed:(int32_t)seed NS_DESIGNATED_INITIALIZER;
+
+@end
+
+/**
+ * Produces a single, constant value at all positions in the space.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKConstantNoiseSource : GKNoiseSource
+
+@property (nonatomic) double value;
+
++ (instancetype)constantNoiseWithValue:(double)value;
+- (instancetype)initWithValue:(double)value NS_DESIGNATED_INITIALIZER;
+
+@end
+
+/**
+ * Produces 3D cylindrical noise with an infinite number of cylinders-within-cyliners of constantly-increasing radius.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKCylindersNoiseSource : GKNoiseSource
+
+@property (nonatomic) double frequency;
+
++ (instancetype)cylindersNoiseWithFrequency:(double)frequency;
+- (instancetype)initWithFrequency:(double)frequency NS_DESIGNATED_INITIALIZER;
+
+@end
+
+/**
+ * Produces 3D spherical noise with an infinite number of spheres-within-spheres of constantly-increasing radius.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKSpheresNoiseSource : GKNoiseSource
+
+@property (nonatomic) double frequency;
+
++ (instancetype)spheresNoiseWithFrequency:(double)frequency;
+- (instancetype)initWithFrequency:(double)frequency NS_DESIGNATED_INITIALIZER;
+
+@end
+
+/**
+ * Produces noise in a checkerboard pattern.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKCheckerboardNoiseSource : GKNoiseSource
+
+@property (nonatomic) double squareSize;
+
++ (instancetype)checkerboardNoiseWithSquareSize:(double)squareSize;
+- (instancetype)initWithSquareSize:(double)squareSize NS_DESIGNATED_INITIALIZER;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKObstacle.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKObstacle.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKObstacle.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKObstacle.h	2016-05-25 04:45:23.000000000 +0200
@@ -1,11 +1,11 @@
 //
 //  GKObstacle.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright © 2015 Apple. All rights reserved.
 //
 
-#import <simd/simd.h>
+#import <GameplayKit/GameplayKitBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -44,7 +44,7 @@
 /**
  * An obstacle with an impassible closed polygon
  */
-GK_BASE_AVAILABILITY @interface GKPolygonObstacle : GKObstacle
+GK_BASE_AVAILABILITY @interface GKPolygonObstacle : GKObstacle <NSCoding>
 
 /**
  * Number of vertices on this polygon
@@ -67,5 +67,26 @@
 
 @end
 
+/**
+ * An obstacle with an impassible radius in 3D space
+ * For use with GKAgent3D.  Using this with a GKAgent2D is no different than using GKCircleObstacle.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKSphereObstacle : GKObstacle
+
+/**
+ * Radius of the impassible circle
+ */
+@property (nonatomic, assign) float radius;
+
+/**
+ * Position of the center of the circle in 3D space.
+ */
+@property (nonatomic, assign) vector_float3 position;
+
++ (instancetype)obstacleWithRadius:(float)radius;
+- (instancetype)initWithRadius:(float)radius NS_DESIGNATED_INITIALIZER;
+
+@end
+
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKObstacleGraph.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKObstacleGraph.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKObstacleGraph.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKObstacleGraph.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1,131 @@
+//
+//  GKObstacleGraph.h
+//  GameplayKit
+//
+//  Copyright © 2015 Apple. All rights reserved.
+//
+
+#import <GameplayKit/GKGraph.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/**
+ * A collection of GKGraphNodes that are governed by a set of extruded GKPolygonObstacles
+ */
+GK_BASE_AVAILABILITY @interface GKObstacleGraph<NodeType : GKGraphNode2D*> : GKGraph
+
+/*
+ * Array of the extruded obstacles currently represented by this graph
+ */
+@property (nonatomic, readonly, nonnull) NSArray<GKPolygonObstacle *> *obstacles;
+
+/*
+ * The distance by which all obstacles are extruded.
+ * This is most commonly the spatial bounding radius of a potential traveler on this path
+ */
+@property (nonatomic, readonly) float bufferRadius;
+
+/**
+ * Creates an optimal bidirectional graph based on a list of obstacles.
+ * Each vertex of each obstacle is extruded and a connection is made between each vertex that does not intersect an obstacle
+ * Guaranteed not to have any edges which intersect obstacles.
+ * Same effect as [[GKObstacleGraph alloc] init], setting bufferRadius, and then calling addObstacles.
+ * @param obstacles a list of obstacles to create the graph from
+ * @param bufferRadius the circular radius of a potential agent that will navigate this graph.  Obstacles are extruded by this amount to create the graph.  Must be positive.  Negative values are clipped to 0.0f
+ */
++ (instancetype)graphWithObstacles:(NSArray<GKPolygonObstacle *> *)obstacles bufferRadius:(float)bufferRadius;
+- (instancetype)initWithObstacles:(NSArray<GKPolygonObstacle *> *)obstacles  bufferRadius:(float)bufferRadius;
+
+/**
+ * Creates an optimal bidirectional graph based on a list of obstacles.
+ * Each vertex of each obstacle is extruded and a connection is made between each vertex that does not intersect an obstacle
+ * Guaranteed not to have any edges which intersect obstacles.
+ * Same effect as [[GKObstacleGraph alloc] init], setting bufferRadius, and then calling addObstacles.
+ * @param obstacles a list of obstacles to create the graph from
+ * @param bufferRadius the circular radius of a potential agent that will navigate this graph.  Obstacles are extruded by this amount to create the graph.  Must be positive.  Negative values are clipped to 0.0f
+ * @param nodeClass the class of the nodes that this graph should create.  Must descend from GKGraphNode2D
+ */
++ (instancetype)graphWithObstacles:(NSArray<GKPolygonObstacle *> *)obstacles bufferRadius:(float)bufferRadius nodeClass:(Class)nodeClass;
+- (instancetype)initWithObstacles:(NSArray<GKPolygonObstacle *> *)obstacles  bufferRadius:(float)bufferRadius nodeClass:(Class)nodeClass;
+
+
+/**
+ * Connects the node to this graph by testing edge intersection with existing obstacles.
+ * Same behavior as if this node had been present during initWithObstacles.
+ * @param node the node to connect
+ */
+- (void)connectNodeUsingObstacles:(NodeType)node;
+
+/**
+ * Same behavior as connectNodeUsingObstacles: except you can optionally ignore certain obstacles from being tested for intersection.
+ */
+- (void)connectNodeUsingObstacles:(NodeType)node ignoringObstacles:(NSArray<GKPolygonObstacle *> *)obstaclesToIgnore;
+
+/**
+ * Same behavior as connectNodeUsingObstacles: except you can optionally ignore the bounding radius of certain obstacles from being tested for intersection
+ */
+- (void)connectNodeUsingObstacles:(NodeType)node ignoringBufferRadiusOfObstacles:(NSArray<GKPolygonObstacle *> *)obstaclesBufferRadiusToIgnore;
+
+/**
+ * Adds obstacles to this graph.
+ * Obstacle is extruded and graph nodes are generated from its vertices and then connected to this graph
+ * Nothing is done if an obstacle is already present in this graph
+ * Any existing connections that intersect the new obstacles are destroyed unless they are protected with [GKObstacleGraph lockConnection:]
+ * @param obstacles an array of obstacles to be added
+ * @see lockConnection
+ */
+- (void)addObstacles:(NSArray<GKPolygonObstacle *> *)obstacles;
+
+/**
+ * Removes obstacles from this graph.
+ * All associated graph nodes are removed and their connections are bidirectionally removed.
+ * Connections between obstacle nodes that were previously invalidated by any of these obstacles are restored.
+ * Nothing is done if an obstacle is already present in this graph
+ * @param obstacles an array of obstacles to be removed
+ */
+- (void)removeObstacles:(NSArray<GKPolygonObstacle *> *) obstacles;
+
+/**
+ * Removes all obstacles from this graph.
+ */
+- (void)removeAllObstacles;
+
+/**
+ * Returns an array of the graph nodes associated with a given obstacle
+ * @param obstacle the obstacle who's nodes are to be retrieved
+ */
+-(NSArray<NodeType> *)nodesForObstacle:(GKPolygonObstacle *)obstacle;
+
+/**
+ * Marks a connection as "locked", preventing this connection from being destroyed when you add obstacles that would intersect it
+ * @param startNode startNode of the connection to lock
+ * @param endNode endNode of the connection to lock
+ */
+- (void)lockConnectionFromNode:(NodeType)startNode toNode:(NodeType)endNode;
+
+/**
+ * "Unlocks" a connection, removing its protection from being destroyed when you add obstacles that would intersect it
+ * @param startNode startNode of the connection to unlock
+ * @param endNode endNode of the connection to unlock
+ * @see lockConnection
+ */
+- (void)unlockConnectionFromNode:(NodeType)startNode toNode:(NodeType)endNode;
+
+/**
+ * Query if a given connection is locked
+ * @param startNode startNode of the connection to query
+ * @param endNode endNode of the connection to query
+ * @see lockConnection
+ * @see unlockConnection
+ * @return YES if the connection was locked with lockConnection, NO if it was never locked or was unlocked via unlockConnection
+ */
+- (BOOL)isConnectionLockedFromNode:(NodeType)startNode toNode:(NodeType)endNode;
+
+/**
+ * Returns the class of the specified generic index
+ */
+- (nonnull Class)classForGenericArgumentAtIndex:(NSUInteger)index;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKOctree.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKOctree.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKOctree.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKOctree.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1,95 @@
+//
+//  GKOctree.h
+//  GameplayKit
+//
+//  Copyright © 2015 Apple. All rights reserved.
+//
+
+#import <GameplayKit/GameplayKitBase.h>
+#import <GameplayKit/GKPrimitives.h>
+
+/**
+ * The individual node(s) that make up a GKOctree.
+ * Used as a hint for faster removal via [GKOctree removeData:WithNode:]
+ */
+GK_BASE_AVAILABILITY_2 @interface GKOctreeNode : NSObject
+
+/* The box associated with this octree node*/
+@property (readonly) struct GKBox box;
+
+@end
+
+
+/**
+ * A tree data structure where each level has 8 children that subdivide a given space into the eight octants.
+ * Stores arbitrary NSObject elements via points and boxes.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKOctree <ElementType: NSObject*> : NSObject
+
+/**
+ * Creates a octree with a given bounding box and minimum allowed cell size
+ *
+ * @param box the bounding box of this octree.  all elements bounding boxes must be within this space.
+ * @param minCellSize the minimum allowed cell size.  The octree will not create octants that have a width,height or depth smaller than this size.
+ */
++(instancetype)octreeWithBoundingBox:(GKBox)box minimumCellSize:(float)minCellSize;
+-(instancetype)initWithBoundingBox:(GKBox)box minimumCellSize:(float)minCellSize;
+
+/**
+ * Adds an NSObject to this octree with a given point.
+ * This element will always reside in the leaf node its point is in.
+ *
+ * @param element the element to be stored
+ * @param point the point associated with the element you want to store
+ * @return the node the element was added to
+ */
+-(GKOctreeNode*)addElement:(ElementType)element withPoint:(vector_float3)point;
+
+/**
+ * Adds an NSObject to this octtree with a given axis-aligned box
+ * This element will reside in the lowest node that it's box fits in completely.
+ *
+ * @param element the element to be stored
+ * @param box the box associated with the element to be stored
+ * @return the node that the element was added to
+ */
+-(GKOctreeNode*)addElement:(ElementType)element withBox:(GKBox)box;
+
+/**
+ * Returns all of the elements in the node this point would be placed in
+ *
+ * @param point the point to query
+ * @return an NSArray of all the element found at the node this point would be placed in
+ */
+-(NSArray<ElementType>*)elementsAtPoint:(vector_float3)point;
+
+/**
+ * Returns all of the elements that resides in nodes which intersect the given box
+ *
+ * @param box the box tha specifies which elements you would like to retrieve
+ * @return an NSArray of all the elements in all of the nodes that intersect the given box
+ *
+ */
+-(NSArray<ElementType>*)elementsInBox:(GKBox)box;
+
+/**
+ * Removes the given NSObject from this octree
+ * Note that this is an exhaustive search and is can be slow for larger trees.
+ * Cache the relevant GKOctreeNode and use removeElement:WithNode: for better performance.
+ *
+ * @param element the element to be removed
+ * @return returns YES if the data was removed, NO otherwise
+ */
+-(BOOL)removeElement:(ElementType)element;
+
+/**
+ * Removes the given NSObject from the given node
+ * Note that this is not an exhaustive search and is faster than removeData:
+ *
+ * @param element the element to be removed
+ * @param node the node in which this data resides
+ * @return returns YES if the element was removed, NO otherwise
+ */
+-(BOOL)removeElement:(ElementType)element withNode:(GKOctreeNode*)node;
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKPath.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKPath.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKPath.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKPath.h	2016-05-25 04:45:23.000000000 +0200
@@ -1,6 +1,6 @@
 //
 //  GKPath.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright © 2015 Apple. All rights reserved.
 //
@@ -9,15 +9,11 @@
 #import <Foundation/Foundation.h>
 #import <simd/simd.h>
 
-@class GKGraphNode2D;
+@class GKGraphNode;
 
 NS_ASSUME_NONNULL_BEGIN
 
-/**
- * Represents a simple polygonal chain in 2D space.
- * Followable by GKAgent's steering functions.
- */
-NS_CLASS_AVAILABLE(10_11, 9_0) @interface GKPath : NSObject
+GK_BASE_AVAILABILITY @interface GKPath : NSObject
 
 /**
  * Radius of the pathway.  Defines a spatial area that the path occupies.
@@ -26,32 +22,47 @@
 @property (nonatomic, assign) float radius;
 
 /**
+ * Number of points in this path
+ */
+@property (readonly) NSUInteger numPoints;
+
+/**
  * Does this path loop back on itself, creating a cycle?
  */
 @property (nonatomic, assign, getter=isCyclical) BOOL cyclical;
 
 /**
- * Number of points in this path
+ * Creates a path from an array of points
+ * @param points an array of points to make a path from
+ * @param radius radius of the path to create
+ * @param cyclical is the path a cycle that loops back on itself?
  */
-@property (readonly) NSUInteger numPoints;
-
 + (instancetype)pathWithPoints:(vector_float2 *)points count:(size_t)count radius:(float)radius cyclical:(BOOL)cyclical;
-- (instancetype)initWithPoints:(vector_float2 *)points count:(size_t)count radius:(float)radius cyclical:(BOOL)cyclical NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithPoints:(vector_float2 *)points count:(size_t)count radius:(float)radius cyclical:(BOOL)cyclical;
++ (instancetype)pathWithFloat3Points:(vector_float3 *)points count:(size_t)count radius:(float)radius cyclical:(BOOL)cyclical NS_AVAILABLE(10_12, 10_0);
+- (instancetype)initWithFloat3Points:(vector_float3 *)points count:(size_t)count radius:(float)radius cyclical:(BOOL)cyclical NS_AVAILABLE(10_12, 10_0);
 
 /**
- * Creates a path from an array of GKGraphNode2D (often a result of pathfinding)
+ * Creates a path from an array of graph nodes (often a result of pathfinding)
+ * Accepts GKGraphNode2D and GKGraphNode3D
  * Cyclical is set to NO
  * @param graphNodes an array of graph nodes to make a path from
  * @param radius radius of the path to create
  * @see GKGraphNode
  */
-+ (instancetype)pathWithGraphNodes:(NSArray<GKGraphNode2D *> *)graphNodes radius:(float)radius;
-- (instancetype)initWithGraphNodes:(NSArray<GKGraphNode2D *> *)graphNodes radius:(float)radius;
++ (instancetype)pathWithGraphNodes:(NSArray<GKGraphNode*> *)graphNodes radius:(float)radius;
+- (instancetype)initWithGraphNodes:(NSArray<GKGraphNode*> *)graphNodes radius:(float)radius;
 
-/**
- * Returns the point at the given index
+/*
+ * Returns the 2D point at the given index.  Returns (x,y,0) if the underlying points are (x,y)
+ */
+-(vector_float2)pointAtIndex:(NSUInteger)index NS_DEPRECATED(10_11, 10_12, 9_0, 10_0);
+-(vector_float2)float2AtIndex:(NSUInteger)index NS_AVAILABLE(10_12, 10_0);
+
+/*
+ * Returns the 3D point at the given index.  Returns (x,y,0) if the underlying points are (x,y)
  */
--(vector_float2)pointAtIndex:(NSUInteger)index;
+-(vector_float3)float3AtIndex:(NSUInteger)index NS_AVAILABLE(10_12, 10_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKPrimitives.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKPrimitives.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKPrimitives.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKPrimitives.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1,33 @@
+//
+//  GKPrimitives.h
+//  GameplayKit
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+
+/**
+ * Representation of an axis aligned box via its min corner (lower-left) and max corner (upper-right) 
+ */
+struct GKBox
+{
+    vector_float3 boxMin;
+    vector_float3 boxMax;
+};
+typedef struct GKBox GKBox;
+
+/**
+ * Representation of an axis aligned quad via its min corner (lower-left) and max corner (upper-right)
+ */
+struct GKQuad
+{
+    vector_float2 quadMin;
+    vector_float2 quadMax;
+};
+typedef struct GKQuad GKQuad;
+
+struct GKTriangle
+{
+    vector_float3 points[3];
+};
+typedef struct GKTriangle GKTriangle;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKQuadtree.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKQuadtree.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKQuadtree.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKQuadtree.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1,95 @@
+//
+//  GKQuadTree.h
+//  GKQuadTreeTest
+//
+//  Copyright © 2015 Apple Inc. All rights reserved.
+//
+
+#import <GameplayKit/GameplayKitBase.h>
+#import <GameplayKit/GKPrimitives.h>
+
+/**
+ * The individual node(s) that make up a GKQuadtree.
+ * Used as a hint for faster removal via [GKQuadtree removeData:WithNode:]
+ */
+GK_BASE_AVAILABILITY_2 @interface GKQuadtreeNode : NSObject
+
+/* The quad associated with this quad tree node */
+@property (nonatomic, readonly) GKQuad quad;
+
+@end
+
+
+/**
+ * A tree data structure where each level has 4 children that subdivide a given space into the four quadrants.
+ * Stores arbitrary NSObject data via points and quads.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKQuadtree <ElementType : NSObject*>: NSObject
+
+/**
+ * Creates a quadtree with a bounding quad and minimum allowed cell size
+ *
+ * @param quad the quad that specifies of the bounds of this quadtree. Elements must only be within these bounds.
+ * @param minimumCellSize the minimum allowed cell size.  The quadtree will not create quadrants that have a width or height smaller than this size.
+ */
++(instancetype)quadtreeWithBoundingQuad:(GKQuad)quad minimumCellSize:(float)minCellSize;
+-(instancetype)initWithBoundingQuad:(GKQuad)quad minimumCellSize:(float)minCellSize NS_DESIGNATED_INITIALIZER;
+
+/**
+ * Adds an NSObject to this quadtree with a given point.
+ * This data will always reside in the leaf node its point is in.
+ *
+ * @param element the element to store
+ * @param point the point associated with the element you want to store
+ * @return the quadtree node the element was added to
+ */
+-(GKQuadtreeNode*)addElement:(ElementType)element withPoint:(vector_float2)point;
+
+/**
+ * Adds an NSObject to this quadtree with a given quad.
+ * This data will reside in the lowest node that its quad fits in completely.
+ *
+ * @param data the data to store
+ * @param quad the quad associated with the element you want to store
+ * @return the quad tree node the element was added to
+ */
+-(GKQuadtreeNode*)addElement:(ElementType)element withQuad:(GKQuad)quad;
+
+/**
+ * Returns all of the elements in the quadtree node this point would be placed in
+ *
+ * @param point the point to query
+ * @return an NSArray of all the data found at the quad tree node this point would be placed in
+ */
+-(NSArray<ElementType>*)elementsAtPoint:(vector_float2)point;
+
+/**
+ * Returns all of the elements that resides in quad tree nodes which intersect the given quad
+ *
+ * @param quadOrigin the quad you want to test
+ * @return an NSArray of all the elements in all of the nodes that intersect the given quad
+ *
+ */
+-(NSArray<ElementType>*)elementsInQuad:(GKQuad)quad;
+
+/**
+ * Removes the given NSObject from this quad tree.
+ * Note that this is an exhaustive search and is slow.
+ * Cache the relevant GKQuadTreeNode and use removeElement:WithNode: for better performance.
+ *
+ * @param element the data to be removed
+ * @return returns YES if the data was removed, NO otherwise
+ */
+-(BOOL)removeElement:(ElementType)element;
+
+/**
+ * Removes the given NSObject from the given quadtree node
+ * Note that this is not an exhaustive search and is faster than removeData:
+ *
+ * @param element the element to be removed
+ * @param node the node in which this data resides
+ * @return returns YES if the data was removed, NO otherwise
+ */
+-(BOOL)removeElement:(ElementType)data withNode:(GKQuadtreeNode*)node;
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRTree.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRTree.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRTree.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRTree.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1,76 @@
+//
+//  GKRTree.h
+//  GameplayKit
+//
+//  Copyright © 2015 Apple. All rights reserved.
+//
+
+#import <GameplayKit/GameplayKitBase.h>
+#import <GameplayKit/GKPrimitives.h>
+
+/** Used to adjust the way in which RTree nodes are split when they grow too large.
+ 
+ @enum GKRTreeSplitStrategyHalve Specifies that nodes should be split in half based on insert order.
+ @enum GKRTreeSplitStrategyLinear Specifies that nodes should be split along the best dividing axis.
+ @enum GKRTreeSplitStrategyQuadratic Specifies that nodes should be split into groups with the least area.
+ @enum GKRTreeSplitStrategyReduceOverlap Specifies that nodes should be split as to reduce overlap.
+ */
+typedef NS_ENUM(NSInteger, GKRTreeSplitStrategy) {
+    GKRTreeSplitStrategyHalve = 0,
+    GKRTreeSplitStrategyLinear = 1,
+    GKRTreeSplitStrategyQuadratic = 2,
+    GKRTreeSplitStrategyReduceOverlap = 3
+};
+
+
+/**
+ * An R-tree is a data structure that partitions axis aligned bounding rectangles into groups spatially.
+ * When a group goes to large, it is split according to its split strategy into two new groups.
+ * Fast queries can be made on these partition bounding rectangles.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKRTree <ElementType : NSObject*>: NSObject
+
+/**
+ * Amount of array items to reserve before a query.
+ * This improves query performance at the cost of memory
+ */
+@property NSUInteger queryReserve;
+
+/**
+ * Creates an RTree with a given maximum number of children per node.  Nodes that grow beyond this number of children will be split.
+ *
+ * @param maxNumberOfChildren the maximum number of children per node before splitting
+ */
++(instancetype)treeWithMaxNumberOfChildren:(NSUInteger)maxNumberOfChildren;
+-(instancetype)initWithMaxNumberOfChildren:(NSUInteger)maxNumberOfChildren NS_DESIGNATED_INITIALIZER;
+
+/**
+ * Adds an element with the specified bounding rect to this RTree.  The supplied splitting strategy is used if the node this element would be added to needs to be split.
+ *
+ * @param element the element to be added
+ * @param boundingRectMin the min point (lower left) on the bounding rect of the element to be added
+ * @param boundingRectMax the min point (upper right) on the bounding rect of the element to be added
+ * @param splitStrategy the splitting strategy to be used if the node this element would be added to needs to be split
+ */
+-(void)addElement:(ElementType)element boundingRectMin:(vector_float2)boundingRectMin boundingRectMax:(vector_float2)boundingRectMax splitStrategy:(GKRTreeSplitStrategy)splitStrategy;
+
+/**
+ * Removes an element with the specified bounding rect from this RTree.
+ *
+ * @param element the element to be removed
+ * @param boundingRectMin the min point (lower left) on the bounding rect of the element to be removed
+ * @param boundingRectMax the min point (upper right) on the bounding rect of the element to be removed
+ */
+-(void)removeElement:(ElementType)element boundingRectMin:(vector_float2)boundingRectMin boundingRectMax:(vector_float2)boundingRectMax;
+
+/**
+ * Queries all the elements that are in this RTree within the given bounding rect.
+ *
+ * @param min the min point (lower left) of the rect to query
+ * @param rectMax the max point (upper right) of the rect to query
+ *
+ * @return an NSArray of all of the elements that fall within the query rect
+ */
+-(NSArray<ElementType>*)elementsInBoundingRectMin:(vector_float2)rectMin rectMax:(vector_float2)rectMax;
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRandomDistribution.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRandomDistribution.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRandomDistribution.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRandomDistribution.h	2016-05-14 11:24:57.000000000 +0200
@@ -1,6 +1,6 @@
 //
 //  GKRandomDistribution.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright © 2015 Apple. All rights reserved.
 //
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRandomSource.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRandomSource.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRandomSource.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRandomSource.h	2016-05-25 04:45:23.000000000 +0200
@@ -1,12 +1,11 @@
 //
 //  GKRandomSource.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright (c) 2014 Apple. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
-#import "GameplayKitBase.h"
+#import <GameplayKit/GameplayKitBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -132,6 +131,20 @@
 
 @end
 
+@interface NSArray<ObjectType> (GameplayKit)
+
+/*
+ * Returns a shuffled instance of this array using the given random source.
+ */
+- (NSArray<ObjectType>*)shuffledArrayWithRandomSource:(GKRandomSource*)randomSource;
+
+/*
+ * Returns a shuffled instance of this array using the systems underlying random source, as with [GKRandomSource sharedRandom]
+ */
+- (NSArray<ObjectType>*)shuffledArray;
+
+@end
+
 
 /**
  * A deterministic pseudo-random source that generates random numbers based on an arc4 algorithm.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKSKNodeComponent.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKSKNodeComponent.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKSKNodeComponent.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKSKNodeComponent.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1,45 @@
+//
+//  GKSKNodeComponent.h
+//  GameplayKit
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <GameplayKit/GKComponent.h>
+#import <GameplayKit/GKAgent.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class SKNode;
+
+/**
+ A component that encapsulates a SpriteKit node.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKSKNodeComponent : GKComponent <GKAgentDelegate>
+
+/**
+ * Creates a component that encapsulate the given SpriteKit node. When the component is 
+ * added to an entity, the SKNode's entity property will be set.
+ *
+ * @param node Node to associate with the component.
+ * @see SKNode.entity
+ */
++ (instancetype)componentWithNode:(SKNode *)node;
+
+/**
+ * Initializes component to encapsulate the given SpriteKit node. When the component is
+ * added to an entity, the SKNode's entity property will be set.
+ *
+ * @param node Node to associate with the component.
+ * @see SKNode.entity
+ */
+- (instancetype)initWithNode:(SKNode *)node;
+
+/**
+ * The SpriteKit node this component encapsulates.
+ */
+@property (nonatomic, strong) SKNode *node;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKScene.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKScene.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKScene.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKScene.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1,80 @@
+//
+//  GKScene.h
+//  GameplayKit
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <GameplayKit/GameplayKitBase.h>
+
+@class GKEntity, GKGraph;
+
+NS_ASSUME_NONNULL_BEGIN
+
+/**
+ Protocol that specifies the type of objects that can be used as root nodes of a GKScene.
+ 
+ @see GKScene.rootNode
+ */
+@protocol GKSceneRootNodeType <NSObject>
+
+@end
+
+/**
+ A scene stores and handles loading of data related to a particular scene.
+ */
+GK_BASE_AVAILABILITY_2 @interface GKScene : NSObject <NSCopying, NSCoding>
+
+/**
+ Loads a scene from a file contained within the bundle.
+ */
++ (nullable instancetype)sceneWithFileNamed:(NSString *)filename;
+
+/**
+ The entities of this scene.
+ */
+@property (nonatomic, readonly) NSArray<GKEntity *> *entities;
+
+/**
+ The root node for the scene.
+ 
+ @see GKSceneRootNodeType
+ */
+@property (nonatomic, nullable) id <GKSceneRootNodeType> rootNode;
+
+/**
+ The navigational graphs of this scene.
+ */
+@property (nonatomic, readonly) NSArray<GKGraph *> *graphs;
+
+/**
+ Adds an entity to the scene's list of entities.
+ 
+ @param entity the entity to add.
+ */
+- (void)addEntity:(GKEntity *)entity;
+
+/**
+ Removes an entity from the scene's list of entities.
+ 
+ @param entity the entity to remove.
+ */
+- (void)removeEntity:(GKEntity *)entity;
+
+/**
+ Adds a graph to the scene's list of graphs.
+ 
+ @param graph the graph to add.
+ */
+- (void)addGraph:(GKGraph *)graph;
+
+/**
+ Removes a graph from the scene's list of graphs.
+ 
+ @param graph the graph to remove.
+ */
+- (void)removeGraph:(GKGraph *)graph;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKState.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKState.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKState.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKState.h	2016-05-25 04:45:23.000000000 +0200
@@ -1,6 +1,6 @@
 //
 //  GKState.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright (c) 2014 Apple. All rights reserved.
 //
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKStateMachine.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKStateMachine.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKStateMachine.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKStateMachine.h	2016-05-25 04:45:23.000000000 +0200
@@ -1,6 +1,6 @@
 //
 //  GKStateMachine.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright (c) 2014 Apple. All rights reserved.
 //
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKStrategist.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKStrategist.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKStrategist.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKStrategist.h	2016-05-25 04:45:23.000000000 +0200
@@ -1,6 +1,6 @@
 //
 //  GKStrategist.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright (c) 2015 Apple. All rights reserved.
 //
@@ -28,4 +28,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
+NS_ASSUME_NONNULL_END
\ No newline at end of file
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKVersion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKVersion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKVersion.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKVersion.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1 @@
+#define GK_VERSION 60000000
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GameplayKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GameplayKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GameplayKit.h	2015-10-24 00:58:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GameplayKit.h	2016-05-25 04:45:23.000000000 +0200
@@ -1,6 +1,6 @@
 //
 //  GameplayKit.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright (c) 2014 Apple. All rights reserved.
 //
@@ -12,16 +12,32 @@
 #import <GameplayKit/GKAgent.h>
 #import <GameplayKit/GKBehavior.h>
 #import <GameplayKit/GKComponent.h>
+#import <GameplayKit/GKCompositeBehavior.h>
 #import <GameplayKit/GKEntity.h>
 #import <GameplayKit/GKGameModel.h>
 #import <GameplayKit/GKGoal.h>
 #import <GameplayKit/GKGraph.h>
+#import <GameplayKit/GKGridGraph.h>
+#import <GameplayKit/GKObstacleGraph.h>
 #import <GameplayKit/GKGraphNode.h>
 #import <GameplayKit/GKStrategist.h>
+#import <GameplayKit/GKMeshGraph.h>
 #import <GameplayKit/GKMinmaxStrategist.h>
+#import <GameplayKit/GKMonteCarloStrategist.h>
+#import <GameplayKit/GKDecisionTree.h>
+#import <GameplayKit/GKNoiseSource.h>
+#import <GameplayKit/GKNoise.h>
+#import <GameplayKit/GKNoiseMap.h>
 #import <GameplayKit/GKObstacle.h>
+#import <GameplayKit/GKOctree.h>
 #import <GameplayKit/GKPath.h>
+#import <GameplayKit/GKPrimitives.h>
+#import <GameplayKit/GKQuadtree.h>
 #import <GameplayKit/GKRandomDistribution.h>
+#import <GameplayKit/GKRTree.h>
 #import <GameplayKit/GKRuleSystem.h>
 #import <GameplayKit/GKState.h>
 #import <GameplayKit/GKStateMachine.h>
+#import <GameplayKit/GKScene.h>
+#import <GameplayKit/GKSKNodeComponent.h>
+#import <GameplayKit/SpriteKit+Additions.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GameplayKitBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GameplayKitBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GameplayKitBase.h	2015-10-02 23:34:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GameplayKitBase.h	2016-05-25 04:45:23.000000000 +0200
@@ -1,6 +1,6 @@
 //
 //  GameplayKitBase.h
-//  GameLogic
+//  GameplayKit
 //
 //  Copyright (c) 2014 Apple. All rights reserved.
 //
@@ -10,6 +10,8 @@
 #import <Availability.h>
 #import <TargetConditionals.h>
 
+#import <GameplayKit/GKVersion.h>
+
 //Exporting
 #ifdef __cplusplus
 #define GK_EXPORT extern "C" __attribute__((visibility ("default")))
@@ -19,6 +21,7 @@
 
 //Availability
 #define GK_BASE_AVAILABILITY NS_CLASS_AVAILABLE(10_11, 9_0)
+#define GK_BASE_AVAILABILITY_2 NS_CLASS_AVAILABLE(10_12, 10_0)
 
 #define GK_AVAILABLE __OSX_AVAILABLE_STARTING
 
@@ -28,3 +31,6 @@
 //Branch prediction
 #define GK_LIKELY(x)    __builtin_expect(!!(x), 1)
 #define GK_UNLIKELY(x)  __builtin_expect(!!(x), 0)
+
+// Attribute annotation to parse properties from GKComponent derived component classes
+#define GKInspectable __attribute__((annotate("gk_inspectable")))
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/SpriteKit+Additions.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/SpriteKit+Additions.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/SpriteKit+Additions.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/SpriteKit+Additions.h	2016-05-25 04:45:23.000000000 +0200
@@ -0,0 +1,97 @@
+/**
+ @header
+ 
+ 
+ SpriteKit framework category additions related to GameplayKit integration.
+ 
+ 
+ @copyright 2016 Apple, Inc. All rights reserve.
+ 
+ */
+
+#import <SpriteKit/SpriteKit.h>
+
+#import <GameplayKit/GKEntity.h>
+#import <GameplayKit/GKNoiseMap.h>
+#import <GameplayKit/GKObstacle.h>
+#import <GameplayKit/GKScene.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface SKNode (GameplayKit)
+
+/**
+ * Returns an array of GKPolygonObstacles from a group of SKSpriteNode's textures in scene space.
+ *
+ * @see GKObstacleGraph
+ */
++ (NSArray<GKPolygonObstacle*> *)obstaclesFromSpriteTextures:(NSArray<SKNode*>*)sprites accuracy:(float)accuracy;
+
+/**
+ * Returns an array of GKPolygonObstacles from a group of SKNode's transformed bounds in scene space.
+ *
+ * @see GKObstacleGraph
+ */
++ (NSArray<GKPolygonObstacle*> *)obstaclesFromNodeBounds:(NSArray<SKNode*>*)nodes;
+
+/**
+ * Returns an array of GKPolygonObstacles from a group of SKNode's physics bodies in scene space.
+ *
+ * @see GKObstacleGraph
+ */
++ (NSArray<GKPolygonObstacle*> *)obstaclesFromNodePhysicsBodies:(NSArray<SKNode*>*)nodes;
+
+/**
+ * The GKEntity associated with the node via a GKSKNodeComponent.
+ *
+ * @see GKEntity
+ */
+@property (nonatomic, weak) GKEntity *entity NS_AVAILABLE(10_12, 10_0);
+
+@end
+
+/**
+ * Adds conformance to GKSceneRootNodeType for usage as rootNode of GKScene 
+ */
+@interface SKScene (GameplayKit) <GKSceneRootNodeType>
+
+@end
+
+@interface SKTileMapNode (GameplayKit)
+
+/**
+ * Create a set of layered tile map nodes with the specified tile set and dimensions, and fill each layer based on the provided noise map. Each 
+ * layer will be partially filled with a tile group using values from the noise map that fall below the corresponding values in the thresholds 
+ * array. The values in the noise map range from -1 to 1, and the provided threshold values are implicitly bounded with the values -1.0 and 1.0. 
+ * Each threshold value corresponds with a tile group in the tile set, starting with the first tile group in the set. If, for example, we passed 
+ * in a thresholds array with the values [-0.5, 0.0, 0.5], this method would return an array of four tile maps. The first tile map would contain 
+ * the first tile group (i.e., tileSet.tileGroups[0]) within tiles that fall between the threshold values -1.0 and -0.5 in the noise map. The 
+ * second tile map would contain the second tile group (i.e., tileSet.tileGroups[1]) within tiles that fall between the threshold values -0.5 and 
+ * 0.0 in the noise map. The third tile map would contain the third tile group (i.e., tileSet.tileGroups[2]) within tiles that fall between the 
+ * threshold values 0.0 and 0.5 in the noise map. And finally, the fourth tile map would contain the fourth tile group 
+ * (i.e., tileSet.tileGroups[3]) within tiles that fall between the threshold values 0.5 and 1.0.
+ *
+ * @param tileSet the tile set that is used to render the tiles
+ * @param columns the number of columns in each map that can hold tiles
+ * @param rows the number of rows in each map that can hold tiles
+ * @param tileSize the size of each tile in points
+ * @param noiseMap the noise map we wish to use to fill each layer
+ * @param thresholds the thresholds for each tile group in the tile set
+ */
++ (NSArray<SKTileMapNode *> *)tileMapNodesWithTileSet:(SKTileSet *)tileSet columns:(NSUInteger)columns rows:(NSUInteger)rows tileSize:(CGSize)tileSize fromNoiseMap:(GKNoiseMap *)noiseMap tileTypeNoiseMapThresholds:(NSArray<NSNumber *> *)thresholds;
+
+@end
+
+
+@interface SKTexture (GameplayKit)
+
+/**
+ * Create a texture from a GKNoiseMap.
+ *
+ * @param noiseMap the GKNoiseMap from which to create the texture.
+ */
++ (instancetype)textureWithNoiseMap:(GKNoiseMap *)noiseMap NS_AVAILABLE(10_12, 10_0);
+
+@end
+
+NS_ASSUME_NONNULL_END

```