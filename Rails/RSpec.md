# RSpec

#### refactoring_for_inheritance.rb
``` ruby
class MotorVehicle
    attr_reader :color, :wheels
    attr_accessor :status

    def initialize(args)
        @color = args[:color]
        @wheels = args[:wheels]
        post_initialize(args)
    end

    def post_initialize(args); nil; end

    def brake
        self.status = :stopped      
    end
end


class Car < MotorVehicle

    def post_initialize(args)
        @wheels = 4
        @status = :stopped
    end

    def drive
        self.status = :driving
    end

    def needs_gas?
        return [true,true,false].sample
    end

end


class Bus < MotorVehicle
    attr_reader :num_seats
    attr_accessor :passengers, :fare

    def post_initialize(args)
        @wheels = args[:wheels]
        @num_seats = args[:num_seats]
        @fare = args[:fare]
        @passengers=[]
        @status = :stopped
    end

    def drive
        return self.brake if stop_requested?
        self.status = :driving
    end

    def admit_passenger(passenger,money)
        self.passengers << passenger if money >= self.fare
    end

    def stop_requested?
        return [true,false].sample
    end

    def needs_gas?
        return [true,true,true,false].sample
    end
end


class Motorbike < MotorVehicle

    attr_accessor :speed

    def post_initialize(args)
        @wheels = 2
    end

    def drive
        self.status = :driving
        self.speed = :fast
    end

    def brake
        self.status = :stopped 
        self.speed = :none
    end
    def needs_gas?
        return [true,false,false,false].sample
    end 
    def weave_through_traffic
        self.status = :driving_like_a_crazy_person
    end
end
```

#### refactoring_for_inheritance_spec.rb
``` ruby
require_relative 'refactoring_for_inheritance'
require 'rspec'

describe Car do 

  before :each do 
    @the_car = Car.new({color: 'black'}) 
  end

  it "should drive" do
    @the_car.drive
    @the_car.status.should == :driving
  end

  it "should have wheels" do
    @the_car.wheels.should == 4
  end

  it "should have a color" do
    @the_car.color.should == 'black'
  end

  it "should brake" do
    @the_car.brake
    @the_car.status.should == :stopped
  end

  it "should have a gas status" do
    [true,false].include?(@the_car.needs_gas?).should == true
  end

end

describe Bus do 

  before :each do
    @the_bus = Bus.new({color: 'black', wheels: 8, num_seats: 50, fare: 5})
  end

  it "should have seats" do
    @the_bus.num_seats.should == 50
  end

  it "should have a fare" do
    @the_bus.fare.should == 5
  end

  it "should have & admit passengers" do
    @the_bus.admit_passenger('John Smith', 5)
    @the_bus.passengers.length.should == 1
  end

  it "should respond to stop requests" do
    [true,false].include?(@the_bus.stop_requested?).should == true
  end

  # SHARED

  it "should have a color" do
    @the_bus.color.should == 'black'
  end

  it "should have wheels" do
    @the_bus.wheels.should == 8
  end

  it "should brake" do
    @the_bus.brake
    @the_bus.status.should == :stopped
  end

  it "should have a gas status" do
    [true,false].include?(@the_bus.needs_gas?).should == true
  end

end

describe Motorbike do 

  before :each do
    @the_motorbike = Motorbike.new({color: 'black'})
  end

  it 'should have a speed' do
    @the_motorbike.drive
    @the_motorbike.speed.should == :fast
  end

  it 'should be able to weave through traffic' do
    @the_motorbike.weave_through_traffic
    @the_motorbike.status.should == :driving_like_a_crazy_person
  end

  it "should have a color" do
    @the_motorbike.color.should == 'black'
  end

  it "should have wheels" do
    @the_motorbike.wheels.should == 2
  end

  it "should brake" do
    @the_motorbike.brake
    @the_motorbike.status.should == :stopped
  end

  it "should have a gas status" do
    [true,false].include?(@the_motorbike.needs_gas?).should == true
  end

end
```